# 2 Host Vars and Templates

Nodes of a cluster typically follow the same configuration except for some
minor differences. For instance, you may want a cluster where each node has the
`tree` command installed but, of course, each node would still have its own
hostname configured. At this point, you know how to make a cluster that is
_exactly_ the same with each other. In this section, you will learn how to make
node-specific changes.

## Host Vars

Host vars are (for now) defined in the playbook in its own section. You can pass
these variables as arguments to modules. For example, to create a user with a
name similar to the hostname you can do as follows

```yaml
---
- hosts: messi
  vars:
    hostname: messi
  tasks:
    - name: create user with name similar to hostname
      user:
        name: "{{ hostname }}"
```

## Templating

We have already introduced the `lineinfile` module. While this lets us write to
files, it is awkward what we want to write something more than one line. Thus,
Ansible has the [template module](https://docs.ansible.com/ansible/latest/modules/template_module.html).

Most server applications are configurable via config text files. As said above,
in a cluster, it is not uncommon to find them differ in subtle ways while being
generally similar in structure. This makes them a good candidate for templating.

Note that you can still refer to host vars inside of templates.

**Demonstration/Exercise:** Your remote should have (had) the text file
`~/the-c-programming-language/hello-world/hello.txt` which just says "Hello
World". Modify you playbook so that it greets your hostname instead. (E.g.,
If your hostname is "iniesta", it will contain the text "Hello iniesta".)

## Exercise

Notice that your remote machines are currently named the default hostname
`vagrant`. Change this to reflect the name given to them in your inventory file.

There is more than one way to do this! Explore the possibilities if one does not
work on your first attempt.

## Documentation

- [Ansible Templating Doc](https://docs.ansible.com/ansible/2.6/user_guide/playbooks_templating.html)
- [Jinja2 Homepage](http://jinja.pocoo.org/)
