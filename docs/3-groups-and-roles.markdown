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

### Exercise

Do you see any problems with the following playbook?

```yaml
---
- hosts: local
  roles:
    - install_needed_programs
    - configure_needed_programs
```

## Tags

Consider the following scenario: you are setting up a DB server from scratch and
you have structured your playbook into roles that do as follows:

- Install and configure your DB of choice.
- Define firewall rules that restrict which servers can connect to your DB.
- Create user accounts for people who are authorized to SSH into the DB server.

(Notice that these "roles" are independent of each other: you can define
firewall rules even if the DB is not yet installed and you can create user
accounts even if the firewall is not yet configured.)

However, during the course of your server's lifetime, several things can happen
that would require you to reprovision your server:

- Your DB of choice might release upgrades which you need to install. Or you
might need to reconfigure your DB so that it can better handle the usage it is
subjected to.
- New servers that need to connect to the DB might be introduced into your
cluster.
- People come and leave so you need to add and revoke access to users.

Each of these scenarios entail reprovisioning your server to accommodate any one
of these changes. (**Remember:** all these scenarios do not happen all at once;
they may happen independently throughout the course of your server's uptime.)
Rerunning the playbook will solve our problems but inefficiently; you do not
want to go through a lengthy installation/configuration phase if all you want
is to remove the SSH credentials of one user.

Ansible handles situations like this via _tags_. Tags are a way to further
modularize your playbook. On top of this, you can use tags to selectively run
parts of your playbook.

In the given scenario above, we can tag the playbook as follows,

```yaml
---
- hosts: local
  roles:
    - role: install_and_configure_db
      tags: db_installation
    - role: define_firewall
      tags: firewall, administrative
    - role: create_user_accounts
      tags: ssh, administrative
```

## Documentation

- [Ansible Roles](https://docs.ansible.com/ansible/2.5/user_guide/playbooks_reuse_roles.html)
- [Ansible Tags](https://docs.ansible.com/ansible/devel/user_guide/playbooks_tags.html)
