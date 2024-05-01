# Ad-hoc commands

Ad-hoc commands are one liners commands where a module is used agains a single or a group of hosts with one return. Ad-hoc commands has the following structure `ansible [hostname | groupname] [-m <module>] [-a "<param1=value1> <param2=value2> ..."]`. On the other hand, playbooks runs a series of tasks and modules. Ad-hoc commands are good for:

- Operational tasks: check logs, status, daemon control, specific operational tasks
- Informational commands: Check installed software, system properties, performance information
- Testing: test modules besor using them in a playbook

# Ansible playbook

Playbooks are good for:

- Deployments
- Routine tasks
- System deployments

`ansible-playbook `

