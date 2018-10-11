# vague rants

A codelab-style tutorial for Ansible.

## Requirements:

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
1. **Spin up the Vagrant box for this repo.** Just do `vagrant up` while at the
root of this repo.
1. **Copy your host _public_ key into the authorized keys of your Vagrant VM.**
Do `vagrant ssh` to get into your Vagrant VM and then edit `~/.ssh/authorized_keys`.
Copy-paste your public key into the bottom of this file.

## Documentation

- [Ansible inventory file](https://docs.ansible.com/ansible/latest/user_guide/intro_inventory.html)
