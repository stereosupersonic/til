# Ansible

https://learnxinyminutes.com/docs/ansible/
## install

```
pip install ansible
```

## Requirement Server

* ssh access
* python

### inventory file (ini-format)

e.g. hosts.ini

```
[app]
192.168.60.5
192.168.60.6
192.168.1.80 ansible_user=stereosonic

[db]
192.168.60.7

# group has all server
[multi:children]
app
db

# variables for all servers
[multi:vars]
ansible_ssh_user=vagrant

```
## set inventory file in ansible.cfg

```
[defaults]
inventory=hosts.ini
```

## ad-hoc commands

ansible -i hosts.ini multi -m ping # uses the ping module

or with  ansible.cfg inventory setting

ansible multi -m ping

ansible multi -a "date" # uses the default module 'command'

ansible multi -m setup # returns all the informations from a server


## useful settings

### -b run as sudo

ansible  multi -b -a "apt-get update"

### limit run to a specific host

ansible multi -a "date" --limit "192.168.60.5"
or
ansible multi -a "date" --limit "*.5"


### forks (parallel execution)

this speeds up the exection

ansible multi -a "date" -f 1 # only one
ansible multi -a "date" -f 4 # four in parallel

## documentation for module

```
ansible-doc <MODUL> # e.g.: ansible-doc service
```

or

https://docs.ansible.com/ansible/latest/collections/ansible/builtin/



## playbooks

convention is to call it main.yml

### yaml

its writen with yaml: https://learnxinyminutes.com/docs/yaml/

boolean: yes, no or true, false

start each file with "---"

### example

```
---
- hosts: all
  become: yes # run with root privileges

  pre_tasks:
    - name: Update APT cache
      apt:
        update_cache: true
        cache_valid_time: 3600

  tasks:
  - name: Ensure chrony (for time synchronization) is installed.
    yum:
      name: chrony
      state: present

  - name: Ensure chrony is running.
    service:
      name: chronyd
      state: started
      enabled: yes
```

### variables

```
---
- hosts: all
  become: yes # run with root privileges

  vars_files:
    - vars.yml

  tasks:
  - name: Creating an empty file
    file:
      path: "{{file_name}}"
      state: touch
```

vars.yml
```
---
file_name: "/tmp/blah
```

### handlers

```
  handlers:
    - name: restart service
      service:
        name: handlers
        state: restarted
        enabled: yes

  tasks:
  - name: install apache
    apt:
      name: apache2
      state: present
    notify: restart service

```


### vault (encrypt keys)

encrypt
```
ansible-vault encrypt vars/api_key.yml
```

run playbook with encrpyted keys

```
ansible-playbook main.yml --ask-vault-pass
```

edit
```
EDITOR=vim ansible-vault edit vars/api_key.yml
```

### debug

```
- name: Get uptime information
  shell: /usr/bin/uptime
  register: uptime

- name: print uptime
  debug:
    var: uptime.stdout
```

## roles

#### structure of a role directory

```
role_name/
  meta/
  tasks/
```


### call a role

```
---
- hosts: all

  vars:
    my_role_variable

  roles:
    - role_name
```

### roles from ansible galaxy

https://galaxy.ansible.com/

define dependencies in requirements.yml
```
---
roles:
  - name: elliotweiser.osx-command-line-tools
    version: 1.0.1
  - name: geerlingguy.dotfiles
```

set roles path in ansible.cfg
```
[defaults]

roles_path = ./roles:/etc/ansible/roles
```

install roles
```
ansible-galaxy install -r requirements.yml
```

## testing

### yaml lint

https://github.com/adrienverge/yamllint

install
```
pip3 install yamllint
```

use
```
yamllint .
```

### ansible syntax check

```
 ansible-playbook main.yml --syntax-check
 ```

### ansible lint

https://ansible-lint.readthedocs.io/en/latest/

install
```
pip3 install ansible-lint
```

lint
```
ansible-lint main.yml
```
