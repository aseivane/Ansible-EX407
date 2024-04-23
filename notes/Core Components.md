# Inventories

Inventories are how Ansible can locate and run against multiple systems, and essentially is a list of servers with groups so you can run automation tasks on multiple hosts at the same time. Once your inventory is defined, you use patterns to select the hosts or groups you want Ansible to run against. The most common formats are INI and YAML. 

*INI* 
```
mail.example.com

[webservers]
foo.example.com
bar.example.com

[dbservers]
one.example.com
two.example.com
three.example.com
```

*YAML* 
```
ungrouped:
  hosts:
    mail.example.com:
webservers:
  hosts:
    foo.example.com:
    bar.example.com:
dbservers:
  hosts:
    one.example.com:
    two.example.com:
    three.example.com:

```
The default location for this file is `/etc/ansible/hosts`. You can specify a different inventory file at the command line using the `-i <path>` option or in configuration using `inventory`. **Using YAML adds consistency since the playbooks are YAML files**

- You can pull inventory dynamically. For example, you can use a dynamic inventory plugin to list resources in one or more cloud providers.

- You can use multiple sources for inventory, including both dynamic inventory and static files.

# Modules

Modules are tools for particular tasks. Ansible modules are units of code that can control system resources or execute system commands. Ansible provides a module library that you can execute directly on remote hosts or through playbooks. You can also write custom modules.

Generally, the modules takes parameters and the return JSON. This output could be used later.

# Variables

Varibles names should be **letters, numbers and underscores**, start with a letter and can by scoped by a group, host or a playbook. It can store configuration values or returned values and can be dictionaries since Module output is JSON.

## Facts
There are some Ansible default variables. Variables related to remote systems are called facts. With facts, you can use the behavior or state of one system as a configuration on other systems. For example `ansible_facts`. Ansible facts are data related to your remote systems, including operating systems, IP addresses, attached filesystems, and more. 

```
ansible localhost -m ansible.builtin.setup
```

Facts are discovered by Ansible automatically when it reaches out to a host. It can take some time and affect performance, so it can be disabled. Also, it can be cached between playbook execution but is no the default behavior.

# Plays and Playbooks

The goal of a play is to map a group of hosts to some well-defined roles and may use one or more modules to achive a desired end state. For example, deploying some files for a web server and check that is running correctly

A playbook is a series of plays. It will run diferrent plays. Following the web server example, a playbook will also deploy a database and other parts of the application for it to run.

# Configuration Files

Ansible look for configuration values in the following order. *So once it finde the value, it uses it.*

- `ANSIBLE_CONFIG`: Environment variable
- `ansible.cfg`: In the current directory
- `.ansible.cfg`: In the home directory
- `/etc/ansible/ansible.cfg`

Commonly used settings
 
- ansible_managed: will insert the value exactly as it is specified in ansible.cfg. 
- forks: enables paralell tasks
- Inventory: modify where ansible looks for the inventory by default