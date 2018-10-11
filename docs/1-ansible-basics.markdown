# 1 Ansible Basics

## Dissecting the Ansible command

```
ansible-playbook -i provision/inventory provision/playbook.yml
```

`-i provision/inventory` specifies the _inventory file_. The inventory file is
simply a list of remote machines which Ansible can operate on.

`provision/playbook.yml` is the _playbook_. Playbooks contain the tasks which
Ansible will run on your remote machines.

## Anatomy of an inventory file

The inventory file could vary between Ansible projects, depending on the plugins
installed. This tutorial uses the default for Ansible.

Notice that:
- inventory items are headed by a _group name_
- an inventory item is made up of an _alias_ and _behavioral inventory parameters_
- aliases need not be legitimate domain names

## Anatomy of a playbook

Playbooks are the "scripts" Ansible runs in your remote machine.

An item in the playbook has two main parts: the tasks to execute and the
information on where and how to run the said tasks.

In turn, a _task_ is divided into two parts: the _name_ and the _module_ for
making the task do something.

## Exercises

1. At this point, the `tree` command in installed in your remote machine. How do
you _uninstall_ `tree` using Ansible?
1. What do you think will happen if you run the playbook to uninstall `tree`
when `tree` is not present? Or if you run the playbook to install `tree` when
`tree` is already present?

## Documentation

- [Ansible inventory file](https://docs.ansible.com/ansible/latest/user_guide/intro_inventory.html)
- [Ansible modules index](https://docs.ansible.com/ansible/2.6/modules/modules_by_category.html)
