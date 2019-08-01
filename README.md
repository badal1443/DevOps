# DevOps
All my DevOps work will be submitted here.

------
**As per architecture We needed 3 machines, (EC2-A, EC2-B and EC2-C).
EC2-A (redhat linux) will be having ansible installed on it.
EC2-B will be used as a machine to install Jenkins tool.
We will generate ssh key on EC2-A , without password and use it to connect to EC2-B machine.**

## Steps to Generate SSH key and adding it to remote server.
**Steps:**
1. Generate ssh key on EC2-A using command *ssh-keygen -t rsa -C "name of the key/identifier"*. It will generate provate and public key at this location. *~/.ssh/*.
2. Copy content of id_rsa.pub.
3. Login to remote machines EC2-B and EC2-C and go to location *~/.ssh/*. open *authorized_keys* file in vi editor using command *sudo vi authorized_keys* and add content of public key into this file and save it.
4. Now you can test if these SSH keys are working for you. Go to EC2-A and run command *ssh <ip_address of EC2-B/EC2-C>*. If successful, then you're all set.

## Steps to add Hosts in ansible file.
**Steps:**


On EC2-A
Goto /etc/ansible directory and run

sudo vi hosts

and add following lines to add new host under a group named yodha.
[yodha]
host1 ansible_ssh_host=34.221.214.11

After making this change. Run a command to see if ansible able to ping EC2-B server.
ansible -m ping all

result:
ec2-user:/etc/ansible $ ansible -m ping all
The authenticity of host '34.221.214.11 (34.221.214.11)' can't be established.
ECDSA key fingerprint is SHA256:Lhpx6Uushgqb6URqSfBkBriTA2O5ZHNCw+IawbaSzuU.
ECDSA key fingerprint is MD5:3c:ad:98:a8:78:04:da:56:5f:b9:5e:14:b3:dd:82:16.
Are you sure you want to continue connecting (yes/no)? yes
host1 | SUCCESS => {
    "changed": false, 
    "ping": "pong"
}


-----------
## First time run of Ansible Playbook

ec2-user:~/environment/GIT/DevOps/ansible (master) $ ansible-playbook playbook_yodha1.yaml
[DEPRECATION WARNING]: Instead of sudo/sudo_user, use become/become_user and make sure become_method is 'sudo' (default). This feature will be removed in 
version 2.6. Deprecation warnings can be disabled by setting deprecation_warnings=False in ansible.cfg.

PLAY [yodha1_apache] ********************************************************************************************************************************************

TASK [Gathering Facts] ******************************************************************************************************************************************
ok: [host1]

TASK [Install apache packages] **********************************************************************************************************************************
ok: [host1]

TASK [ensure httpd is running] **********************************************************************************************************************************
ok: [host1]

PLAY [yodha1_jenkins] *******************************************************************************************************************************************

TASK [Gathering Facts] ******************************************************************************************************************************************
ok: [host2]

TASK [Install yum] **********************************************************************************************************************************************
changed: [host2]

TASK [Download jenkins.repo] ************************************************************************************************************************************
changed: [host2]

TASK [Import Jenkins Key] ***************************************************************************************************************************************
changed: [host2]

TASK [Install Jenkins] ******************************************************************************************************************************************
changed: [host2]

TASK [Start & Enable Jenkins] ***********************************************************************************************************************************
changed: [host2]

TASK [Sleep for 30 seconds and continue with play] **************************************************************************************************************
ok: [host2]

TASK [Get init password Jenkins] ********************************************************************************************************************************
ok: [host2]

TASK [Print init password Jenkins] ******************************************************************************************************************************
ok: [host2] => {
    "result.stdout": "pwd"
}

PLAY RECAP ******************************************************************************************************************************************************
host1                      : ok=3    changed=0    unreachable=0    failed=0   
host2                      : ok=9    changed=5    unreachable=0    failed=0   

---------
