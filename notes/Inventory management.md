# Inventories
An inventory is a list of host that Ansible manages. The default location is `/etc/ansible/hosts` but it can be sapecified wit `-i <inventory-path>`or caonfigured in `ansible.cfg`. It may contain hosts, patterns, groups and variables.

The inventory allows parent/child relationships among groups. in INI format, use the `:children` suffix, in YAML format, use the `children:` entry

Child groups have a couple of properties to note:

- Any host that is a member of a child group is automatically a member of the parent group.
- Groups can have multiple parents and children, but not circular relationships.
- Hosts can also be in multiple groups, but there will only be one instance of a host at runtime. Ansible merges the data from multiple groups.




<table>
<tr>
<th> YAML </th>
<th> INI </th>
</tr>
<tr>
<td>

```yaml
---
all:
  hosts:
    mail.example.com
        ansible_port: 5586
        ansible_host: 192.168.0.10
  children:
    webservers:
      hosts:
        httpd1.example.com
        https2.example.com
      vars:
        http_port: 8080
    labservers:
      hosts:
        lab[01:09].example.com    
---
```

</td>
<td>

```ini
mail.example.com ansible_port=5586 ansible_host=192.168.0.10

[webservers]
httpd1.example.com
https2.example.com

[webservers:vars]
http_port=8080

[labservers]
lab[01:09].example.com   
```

</td>
</tr>
</table>

In YAML inventories, you may terminate hostname entries in the yaml file with a colon as they may contain child elements (host variable definitions). If you intend to use host varaibles, I would recommend terminating all hostname entries with a colon for readability sake.

## Variables
Storing variables in separate host and group variable files is a more robust approach to describing your system policy. Setting variables in the main inventory file is only a shorthand.

Ansible loads host and group variable files by searching paths relative to the inventory file or the playbook file. If your inventory file at `/etc/ansible/hosts` contains a host named ‘labservers’ that belongs to two groups, ‘raleigh’ and ‘webservers’, that host will use variables in YAML files at the following locations:

```
/etc/ansible/group_vars/raleigh # can optionally end in '.yml', '.yaml', or '.json'
/etc/ansible/group_vars/webservers
/etc/ansible/host_vars/foosball
```
For example:
```yaml
script_files: /tmp/usr/local/scripts
```
## Dynamic

Static inventories are predifined where as dynamic are updated using scrips. Dynamics can be any executable script (bash, Python, bin, etc) and returns a JSON containing inventory information. Dynamic inventories are good for cloud environment.

The program/script must respond to two possible parameters: 
- `--list`: provides all the hosts and the invetory with all the usefull data
- `--host [hostname]`: provides data of a particular host

Some of the most used sources:

- Cloud providers
- LDAP
- Cobbler
- Other CMDB software
