# Miscellaneous Notes

## Ansible config

The `ansible-playbook` command already takes in a lot of command line flags that
can change its behavior. If you find yourself constantly using the same flags
to enforce a certain behavior, it might be worthwhile to create an
[Ansible config](https://docs.ansible.com/ansible/2.4/intro_configuration.html)
instead.

Note that Ansible successively looks for config files in the following
locations:

* ANSIBLE_CONFIG (an environment variable)
* ansible.cfg (in the current directory)
* .ansible.cfg (in the home directory)
* /etc/ansible/ansible.cfg
