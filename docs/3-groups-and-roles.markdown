# 3 Groups and Roles

So far, our playbooks have only ever touched one node. Aside from idempotence,
we haven't seen yet how Ansible could have an advantage over plain shell
scripts.

In this section, we will explore some actual, cluster management with Ansible.

## Running playbooks on multiple hosts

There are currently 3 hosts defined in your inventory file:

```
[local]
messi ansible_host=10.11.4.128
coutinho ansible_host=10.11.4.127
rakitic ansible_host=10.11.4.126
```

Given your basic playbook, how can you install `tree` on all your hosts with
just one invocation of `ansible-playbook`?

You can specify multiple hosts in your playbook like so

```yaml
---
- hosts: messi,coutinho,rakitic
```

But of course, this is awkward and unwieldy once you go beyond a handful of
servers. Thankfully, Ansible also accepts a group name as an argument to
`hosts`. Thus you can do:

```yaml
---
- hosts: local
```

## Ansible roles

Often, your infrastructure is not just made up of one cluster/one type of server
configuration. You may want to dedicate a certain cluster for a particular task:
databases are read/write-intensive so you may want them to be separate from your
web servers. This would mean a different kind of configuration altogether.

The customized configuration discussed in the previous section can be described
as _same commands, different arguments_. In contrast, the custom configuration
we want for different clusters will have different commands from the get go
(and, of course, different arguments).

Ansible lets you define roles for your clusters specifically for this purpose.
Note that unlike the mostly free-form directory structure we have been using so
far, using Ansible roles assumes a certain directory structure.

### Relationship between plain playbooks and roles

Notice that the roles directory structure just rearranges the plain playbooks we
are acquainted with so far: in the playbook, we used to have the `tasks` defined
but they are now replaced with `roles`. And then in each role's subdirectory, we
have the `tasks` subdirectory which now contains the steps as outlined in the
`tasks` section of our old playbook!

## Documentation

- [Ansible Roles](https://docs.ansible.com/ansible/2.5/user_guide/playbooks_reuse_roles.html)
