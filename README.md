# DevOps
All my DevOps work will be submitted here.

------
**As per architecture We needed 3 machines, (EC2-A, EC2-B and EC2-C).
EC2-A (redhat linux) will be having ansible installed on it.
EC2-B will be used as a machine to install Jenkins tool.
We will generate ssh key on EC2-A , without password and use it to connect to EC2-B machine.**

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

