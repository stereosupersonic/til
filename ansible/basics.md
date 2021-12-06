# Ansible

## install

```
pip install ansible
```

## Requirement Server

* ssh access
* python

### inventory


##  ad-hoc commands

ansible -i hosts.ini example -m ping # uses the ping module

ansible -i hosts.ini example -a "date" # uses the default module 'command'

ansible -i hosts.ini example -m setup # returns all the informations from a server
