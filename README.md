# Capture Agent Configuration #

Ansible configuration management Galicaster Capture Captures Agents.
This should only be used as an example or referance for your own playbook(s)
and definitely customised for your needs

### Resources ###
* [Ansible](http://docs.ansible.com)

### Running ###
your local host running Ansible version ansible 2.1.2.0 + required
your remote host using ubuntu 16.04
the remote host pre configured with the username `galicaster`
the remote host configured with `root` level key based ssh access
An ssh key file to access the `root` account on the remote client

install the dependancies:

`python -m easy_install --upgrade pyOpenSSL`

`sudo apt-get install openssh-server python-pip`

`sudo pip install ansible`

if you need to set up an ssh keypair on the remote host(s):
```
change to the root user
sudo -i

create the keypair, just follow the instructions
ssh-keygen

Create the authorized_keys file:
touch ~/.ssh/authorized_keys

Set the right permissions:
chmod 600 ~/.ssh/authorized_keys

Add the public key to the authorized_keys file:
cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys

save the private key somewhere safe and never share it.
transfer it to the host that will run the playbook and 
make sure it has the correct permissions for the user using it
example if running on the same machine:
cp ~/.ssh/id_rsa /home/galicaster/
chown galicaster:galicaster /home/galicaster/id_rsa

```

clone this repo onto the machine you want to run it from

`git clone https://github.com/androidwiltron/galicaster-ansible.git`

Move into the ansible playbook directory

`cd galicaster-ansible`

### Out of the Box run ###
you may run this on the same computer its on. not recommended for production however.
normally you would run this from another computer.

to run on localhost:

`cp group_vars/all.example group_vars/all`

edit group_vars/all with a text editor, it will work without editing but you may taylor to your needs.

make sure you can ssh into localhost using `root` account using a private key file
make sure there is a `galicaster` user on the system who is a member of the `sudoers` group

open a terminal session and execute:

`ansible-playbook capture-agent.yml -i hosts --private-key=~/id_rsa`

using any other type of host group or any of the extra vars may make the run fail
without the proper configuration and services being available.


### Run Examples ###
all hosts:
```
ansible-playbook capture-agent.yml -i hosts --private-key=~/id_rsa

```

just a single host using the --limit parameter:
```
ansible-playbook capture-agent.yml -i hosts --private-key=~/id_rsa --limit example-ca

```
limiting the tasks executed to a specific tag:
```
ansible-playbook capture-agent.yml -i hosts --private-key=~/id_rsa --limit example-ca --tags apt,galicaster

```
