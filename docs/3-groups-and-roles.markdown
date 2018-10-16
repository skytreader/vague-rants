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
just on invocation of `ansible-playbook`?

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
