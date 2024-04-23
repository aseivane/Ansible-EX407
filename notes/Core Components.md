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