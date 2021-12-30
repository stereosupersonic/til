# Vagrant

https://www.vagrantup.com/

## setup

brew install vagrant


## find boxes

https://vagrantcloud.com/search

e.g. ubuntu/trusty64

## create a new project

```
vagrant init # creates a Vagrant file inside the current folder
```

config.vm.box = "ubuntu/trusty64"

### Vagrantfile

example with 3 server

```
# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/trusty64"

  config.ssh.insert_key = false

  # Disable automatic box update checking. If you disable this, then
  config.vm.box_check_update = false

  # Disabling the default /vagrant share
  config.vm.synced_folder ".", "/vagrant", disabled: true

  # General VirtualBox VM configuration.
  config.vm.provider :virtualbox do |v|
    v.memory = 256
    v.cpus = 1
    v.linked_clone = true
  end

  config.vm.define "app1" do |app|
    app.vm.hostname = "test-app-1.test"
    config.vm.network "private_network", ip: "192.168.60.5"
  end

  config.vm.define "app2" do |app|
    app.vm.hostname = "test-app-2.test"
    config.vm.network "private_network", ip: "192.168.60.6"
  end

  config.vm.define "db" do |app|
    app.vm.hostname = "test-db.test"
    config.vm.network "private_network", ip: "192.168.60.7"
  end
end
```
## disable known_hosts checking

if you got this error "WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!"

change ~/.ssh/known_hosts
```
Host 192.168.*.*
    StrictHostKeyChecking no
    UserKnownHostsFile /dev/null
```
