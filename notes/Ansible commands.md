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

# Common Modules

## ping

Validate server is up and reachable. The ping command isn't the common ping, it verifies the ability to login and that a usable Python is configured. All the information is [here](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/ping_module.html). Since it uses SSH, another variations of ping needs to bue used for Windows and Network devices.

## setup

Gather sansible facts.

## yum

Use yum package manager to define the state of the package. The arguments are the name of package and the state that is the version. `state=absent` is equivalent to uninstalling it. The flag `-b`is and acronymous of *become user*. If nothing is specified the user assumed is root, but the best practice is use the least priviliged user to acomplish the task.

`ansible <target> -i <inventory> -b -m yum -a "name=git state=latest"`

## service

Control daemon's service.

## user

Control system users. It can create, modify or delete users among other action. The following command adds the user *new-user*. All the things it does are listed [here](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/user_module.html)

`ansible <target> -i <inventory> -b -m user -a "name=new-user"`

## copy

Copy files

## file
Interacts with files. The description and use of the command can be found [here](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/file_module.html). For example, a new file can be created:

`ansible <target> -i <inventory> -m file -a "path=/path/to/file state=touch"`

Or just retrive file information.

`ansible <target> -i <inventory> -m file -a "path=/path/to/file"`

## git

Interact with git repositories
