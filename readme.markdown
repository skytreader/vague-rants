# vague rants

A codelab-style tutorial for Ansible.

## Pre set-up

**Requirements:**

- Ansible 2.7.0
- Vagrant

This tutorial was prepared in an Ubuntu 16.04 environment. Setting this up for
other OSes is definitely possible but is not covered here.

**The first sentence in bold are the general steps you need to accomplish in
your machine.** This is followed by a discussion in normal font which will 
describe in better detail a way to achieve said goal for Ubuntu machines.

1. **Install Ansible.** Install (virtualenv)[https://github.com/brainsik/virtualenv-burrito].
Create a virtualenv for this (`mkvirtualenv vague-rants`) and install ansible
(`pip install ansible==2.7.0`).
1. **Install Vagrant.** You can download a Vagrant binary [here](https://www.vagrantup.com/downloads.html).
Choose one for your distro and copy it to a directory in your `$PATH` (e.g.,
`/usr/local/bin`, `~/bin`, or as I prefer it, in `/opt/bin`).
1. **Spin up the Vagrant box for this repo.** Just do `vagrant up` while at the
root of this repo.

## Documentation

- [Ansible inventory file](https://docs.ansible.com/ansible/latest/user_guide/intro_inventory.html)
