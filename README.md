# Capture Agent Configuration #

Ansible configuration management Galicaster Capture Captures Agents.

### Resources ###
* [Ansible](http://docs.ansible.com)

### Running ###
your local host running Ansible version ansible 2.1.2.0 + required
your remote host using ubuntu 16.04
the remote host pre configured with the username `galicaster`
the remote host configured with `root` level key based ssh access
An ssh key file to access the `root` account on the remote client

### Out of the Box run ###
to run on localhost:
`cp group_vars/all.example group_vars/all`

make sure you can ssh into localhost using `root` account using a private key file
make sure there is a `galicaster` user on the system who is a member of the `sudoers` group

open a terminal session and execute:

`ansible-playbook capture-agent.yml -i hosts --private-key=~/.ssh/private-key-file`

using any other type of host group or any of the extra vars may make the run fail
without the proper configuration and services being available.


### Run Examples ###
all hosts:
```
ansible-playbook capture-agent.yml -i hosts --private-key=~/.ssh/ca-ansible

```

just a single host using the --limit parameter:
```
ansible-playbook capture-agent.yml -i hosts --private-key=~/.ssh/ca-ansible --limit example-ca

```
limiting the tasks executed to a specific tag:
```
ansible-playbook capture-agent.yml -i hosts --private-key=~/.ssh/ca-ansible --limit example-ca --tags apt,galicaster

```
