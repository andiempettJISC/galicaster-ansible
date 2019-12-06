# Capture Agent Configuration #

Ansible configuration management Galicaster Capture Captures Agents.

### Resources ###
* [Ansible](http://docs.ansible.com)

### Running ###
local running Ansible version ansible 2.1.2.0 + required
remote using ubuntu 16.04
remote configured with the user 'galicaster'
remote user configured with root level key based ssh access
An ssh key file to access the root account on the remote client

### Out of the Box run ###
to run on localhost:
`cp all.example all`

make sure you can ssh into localhost using `root` account using a private key file
make sure there is a `galicaster` user on the system who is a member of the `sudoers` group

open a terminal session and execute:

`ansible-playbook capture-agent.yml -i hosts --private-key=~/.ssh/ca-ansible`

using any other type of host group or any of the extra vars may make the run fail
without the proper configuration and services being available.


### Examples ###
all hosts:
```
ansible-playbook capture-agent.yml -i hosts --private-key=~/.ssh/ca-ansible --ask-vault-pass

```

just a single host:
```
ansible-playbook capture-agent.yml -i hosts --private-key=~/.ssh/ca-ansible --ask-vault-pass --limit example-ca

```
specific tag:
```
ansible-playbook capture-agent.yml -i hosts --private-key=~/.ssh/ca-ansible --ask-vault-pass --limit mtt-test-a --tags apt,galicaster

```