# 0 Getting Started

**Motivation:** Ansible is your insurance policy against having a [mystery server](https://www.reddit.com/r/sysadmin/comments/9n48lo/have_you_ever_inherited_the_mystery_server/).

## Terminologies

The _host_ or _host machine_ is the computer you will be running Ansible from.
In this tutorial, this will be whatever computer you are following this tutorial
on (e.g., your laptop).

The _remote machines_ are any number of VMs/servers/cloud instances which you
will be configuring via Ansible. The Vagrant VM specified in this tutorial is
an example of a remote machine (even if it is coexisting in the same hardware
as your host machine or if it is hosted by the same host machine).

## Vagrant commands

All vagrant commands assume the existence of a Vagrantfile in the directory
where the commands are ran.

`vagrant up` Spins up your virtual machine. The first invocation is typically
slow because it downloads the image for the machine (which you probably don't
have yet). Subsequent invocations should be faster since it just turns on the
machine.

`vagrant ssh` SSH into a running VM as the `vagrant` user.

`vagrant halt` Gracefully terminates a running VM.

## Why Ansible?

Ansible tasks and playbooks are, basically, shell scripts for setting up
machines. They are, however more structured than your usual shell script and
pack features that make it ideal for cluster management.

### Advantages

- Unlike shell scripts, Ansible playbooks can be structured such that they are
modular and dependencies are clearly defined.
- Used correctly, it provides replicable steps to set-up your desired
environment.
- Ansible is idempotent: no matter how many times you run an Ansible playbook,
it will result to an identical machine state.

### Disadvantages

- "To fuck up one machine is human; to fuck up an entire cluster is automation."
- Very nitpicky to use correctly (in contrast to following traditional
documentation).

## Demo

1. SSH into the Messi VM and issue the `tree` command. You should get an error that
it does not exist.

```
vague-rants/vms/messi$ vagrant ssh
Welcome to Ubuntu 18.04.1 LTS (GNU/Linux 4.15.0-29-generic x86_64)

...

Last login: Wed Oct 10 22:10:53 2018 from 10.0.2.2
vagrant@vagrant:~$ tree
-bash: tree: command not found
vagrant@vagrant:~$
```

2. Outside your SSH session, in your host machine, do

```
vague-rants$ ansible-playbook -i provision/inventory provision/playbook.yml
```

**Note:** If this is your first time running ansible-playbook, you might be asked
to verify the server you are connecting to (in this case the Vagrant VM).

```
The authenticity of host '10.11.4.128 (10.11.4.128)' can't be established.
ECDSA key fingerprint is SHA256:hNHxoptKsWqkzdME7Bfb+cGjskcAAGySJazK+gDDCHQ.
Are you sure you want to continue connecting (yes/no)?
```

Just say "yes".

3. When the ansible command has successfully finished, SSH into your VM again
and invoke `tree`. The command should now be present.

```
vagrant@vagrant:~$ tree
.

0 directories, 0 files

```
