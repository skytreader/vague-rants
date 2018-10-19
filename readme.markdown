# vague rants

A codelab-style tutorial for Ansible.

## Tutorial Requirements

Software:
- Ansible 2.7.0
- Vagrant

Hardware:
- Please have at least 6-8GB of RAM. The VM itself will take 2GB and that's on
top of whatever other processes you have running in the background.

## Pre set-up

This tutorial was prepared in an Ubuntu 16.04 environment. Setting this up for
other OSes is definitely possible but is not covered here.

**The first sentence in bold are the general steps you need to accomplish in
your machine.** This is followed by a discussion in normal font which will 
describe in better detail a way to achieve said goal for Ubuntu machines.

1. **Install Ansible.** Install [virtualenv](https://github.com/brainsik/virtualenv-burrito).
Create a virtualenv for this (`mkvirtualenv vague-rants`) and install ansible
(`pip install ansible==2.7.0`).
1. **Install VirtualBox.** Downloads are available [here](https://www.virtualbox.org/wiki/Downloads)
for most OS versions.
1. **Install Vagrant.** You can download a Vagrant binary [here](https://www.vagrantup.com/downloads.html).
Choose one for your distro and copy it to a directory in your `$PATH` (e.g.,
`/usr/local/bin`, `~/bin`, or as I prefer it, in `/opt/bin`). Note that,
depending on your machine and VirtualBox, you might have to reconfigure your
BIOS to disable UEFI/SecureBoot.
1. **Generate SSH keys for your host machine, if you haven't already.** You can
follow [this guide](https://www.digitalocean.com/community/tutorials/how-to-set-up-ssh-keys-on-ubuntu-1604)
from DigitalOcean.
1. **Spin up the Vagrant box(es) for this repo.** Just do `vagrant up` while at
the directories of the VMs (clue: they are in the `vms` directory).
1. **Copy your host _public_ key into the authorized keys of your Vagrant VM.**
Do `vagrant ssh` to get into your Vagrant VM and then edit `~/.ssh/authorized_keys`.
Copy-paste your public key into the bottom of this file.

## Following this tutorial in an already-set-up environment

If you have already installed the dependencies mentioned above, you can just
follow these steps to prepare for this tutorial. In any order do as follows:

**Anywhere in your host machine:** Activate the `vague-rants` virtualenv. The
terminal where you do this will be the terminal which you should use to execute
`ansible-playbook` (and `ansible`, in general) commands. Outside this tutorial,
it is still a good idea to use this virtualenv (if maybe renamed) for
interfacing with your actual servers.

```
$ ansible-playbook
ansible-playbook: command not found
$ workon vague-rants
(vague-rants)$ ansible-playbook
Usage: ansible-playbook playbook.yml

Options:
...
```

If you installed virtualenv + virtualenvwrapper via virtualenv-burrito (as
specified in the "Pre set-up" section above), _do not forget to activate your
virtualenvwrapper commands via `source ~/.venvburrito/startup.sh`_. Otherwise,
you won't be able to use commands such as `mkvirtualenv`, `lsvirtualenv`,
`workon`, `deactivate`, etc. (Protip: put it in your `~/.bashrc`.)

**Inside one of the subdirectories in the `vms/` directory of this repo:** Call
`vagrant up`. The first half of this tutorial assumes you have the _messi_ VM
running. The next half needs the two other VMs (_coutinho_ and _rakitic_) but
remember that each of these VMs is a ~2GB tax on your RAM.

Note that in this tutorial, these vagrant instances are our stand-ins for
_actual servers_. You don't need vagrant or any VM to actually work with
Ansible. They are only necessary here for pedagogical purposes.

You are now ready to work through the examples presented in `docs/`.
