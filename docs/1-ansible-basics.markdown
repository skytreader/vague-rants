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

### Exercises

1. At this point, the `tree` command in installed in your Messi VM. How do
you _uninstall_ `tree` using Ansible?
2. What do you think will happen if you run the playbook to uninstall `tree`
when `tree` is not present? Or if you run the playbook to install `tree` when
`tree` is already present?
3. How do make it so that the playbook will also install the `tree` command in
the two other VMs?
4. Explore the file module and make it so that tree will display the following
structure when invoked at the home directory of your remote machine:

```
vagrant@vagrant:~$ tree
.
└── the-c-programming-language
    ├── arrays
    ├── hello-world
    │   └── hello.txt
    ├── pointers
    └── structures

5 directories, 1 file

```

Also, `~/the-c-programming-language/hello-world/hello.txt` should have the
contents "Hello World".

## Behind the scenes

Invoke your `ansible-playbook` command with the `-vvv` flag. That is,

```
ansible-playbook -i provision/inventory -vvv provision/playbook.yml
```

You will notice that each ansible task is actually multiple `ssh` calls behind
the scenes. What this does is to copy a Python script to the remote machine and
run it. (Note that this Python script is actually the _module_ specified in the
task YAML.)

What this implies is that it is good practice to invoke ansible from a machine
that is _in the same network_ as the remote machines it will set-up. This
reduces latency and for long-running jobs, lessens the probability of network
time outs.

## Rerunning playbooks

Ansible is idempotent (unless you use the [command module](https://docs.ansible.com/ansible/2.5/modules/command_module.html)),
which means that repeatedly running a playbook would result in the same machine
state. However, sometimes, an error might occur in the midst of running a
playbook and you need to rerun the playbook after (maybe) debugging the error.
While it is safe to let Ansible run through the tasks it has already done, it
might be too time consuming for you to wait for Ansible to double check on the
machine state.

Ansible provides a couple of ways to save you time. It has the `--start-at-task`
flag:

```
  --start-at-task=START_AT_TASK
                          start the playbook at the task matching this name

```

And it also provides `.retry` files when an error occurs which can be invoked
with the `--limit` flag:

```
  -l SUBSET, --limit=SUBSET
                          further limit selected hosts to an additional pattern
```

### Exercise

Make the playbook you created for Exercise 4 above fail at some point and try to
rerun it without having to go through all the preceeding steps.

## Style guidelines: Looping

You will notice that the given sample answer to Exercise 3 above has a lot of
repeated elements. While this works, this could quickly get tedious and hard to
manage! Not to mention that repeated elements introduces opportunities for error
in your code; imagine mistyping the name of the 28th directory out of 100 you
need to create. Fortunately, Ansible provides us with constructs to _refactor_
our playbooks.

### Exercise

Have a look at [Ansible loops](https://docs.ansible.com/ansible/2.5/user_guide/playbooks_loops.html)
and try to rewrite the `provision/ansible-basics.yml` playbook with less lines.

## Documentation

- [Ansible inventory file](https://docs.ansible.com/ansible/latest/user_guide/intro_inventory.html)
- [Ansible modules index](https://docs.ansible.com/ansible/2.6/modules/modules_by_category.html)
