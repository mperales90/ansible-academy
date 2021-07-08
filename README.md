# Let's install Ansible

There are many ways you can install Ansible, for this demo we will install it with pip. You can check other ways to install it in: 
https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html

Make sure you have python installed:

    python --version 

If you don't, install it with: 

    sudo yum install -y python

Make sure you have pip installed:

    pip--version 

If you don't, install it with: 

    sudo yum install -y python-pip

Install Ansible: 

    pip install ansible

Make sure you have Ansible installed:

    ansible --version 

## Create a Config and Hosts file

As we installed Ansible with pip, there will not be an ansible directorin in etc, we need to create one:

    sudo mkdir /etc/ansible/

Inside this directory, we need to create a config file for Anisble

    sudo vim /etc/ansible/ansible.cfg
> please refer to the ansible.cfg file to review the contents

We also need to create the hosts file

    sudo vim /etc/ansible/hosts
> please refer to the hosts file to review the contents

To validate the above, you can list the hosts defined

    ansible-inventory -y --list

## Connect master and host servers

As Ansible communicates with port 22, you need to add it to the security group inbound rules for master and host to communicate.


**On the master server:** 
Create an SSH key

    ssh-keygen -t rsa
> we created a private and public key, we need to copy the public key to the host server so they can connect
 
**On the host server:** 
Edit the sshd config file:

    sudo vim /etc/ssh/sshd_config

Change PasswordAuthentication param to yes:

	PasswordAuthentication yes

Restart daemon:

    sudo systemctl restart sshd

**On the master server:** 
Copy public key to host

    ssh-copy-id <host_ip>

Validate connection: 

    ansible all -m ping

# Now you can start creating your playbooks 

 1. Create a User
 2. Install a software
 3. Copy files or a directory into the new user’s home directory
 4. Change the permissions and ownership to a file/s
 5. Create a playbook with all the tasks above 
      

## Create the playbooks

Please refer to the playbooks folder for each one.

## Run your playbooks

To run a playbook you need to run the command:

    ansible-playbook <file name>

## Playbook validations

 **Create a User**
 On the host server use below command to validate the current users:

     less /etc/passwd

**Install a software**
Validate if the software is installed with:

    <software> --version

Check if the service is running with: 

    sudo systemctl status <service>

**Copy files or a directory into the new user’s home directory**
Go to the directory where you copied the file and type ls 


**Change the permissions and ownership to a file/s**
Go to the directory of the file and type ll, validate changes are in place

**Create a playbook with all the tasks above**
Open port 80 to your IP in the security group, copy the host public IP and paste it on a browser adding :80 at the end and see your webserver running.
