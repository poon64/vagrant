# vagrant
This is just basic Vagrant with Ansible provisioning to make it easy to spin up a VM for testing. 

Only 2 files are needed. [Vagrantfile](https://www.vagrantup.com/docs/vagrantfile) and [Ansible playbook](http://docs.ansible.com/ansible/latest/playbooks.html). 

## Prereq
- [Vagrant](https://www.vagrantup.com/downloads.html) installed
- Install Vagrant plugins
```
Required 
vagrant plugin install vagrant-proxyconf

Recommend
vagrant plugin install vagrant-multi-putty
vagrant plugin install vagrant-vbguest
```
- Add proxy exception on host node (if needed)
```
export https_proxy=https://proxysesosrv.scania.com:8080
export http_proxy=http://proxysesosrv.scania.com:8080
```
- [VirtualBox](https://www.virtualbox.org/wiki/Downloads) and [VirtualBox Extension Pack](http://download.virtualbox.org/virtualbox/5.1.26/VirtualBox-5.1.26-117224-Win.exe)


## Setup new VM using Vagrant
#### Clone repo
```
git clone git@github.scania.com:sssenz/vagrant.git
```

#### Create new VM with Vagrant
Browse to to the cloned vagrant repo and run:
```
vagrant up
```
This will take some minutes the first time.

#### How to use vagrant
https://www.vagrantup.com/docs/cli/

There are a lot of commands, but here are some common ones.

- `vagrant up [name|id]` - This command creates and configures guest machines according to your Vagrantfile.
- `vagrant halt [name|id]` - This command shuts down the running machine Vagrant is managing.
- `vagrant provision [vm-name]` - Runs any configured provisioners against the running Vagrant managed machine.
- `vagrant ssh [name|id]` - This will SSH into a running Vagrant machine and give you access to a shell.
- 'vagrant init [name' - This initializes the current directory to be a Vagrant environment by creating an initial Vagrantfile if one does not already exist.



## Password
http://docs.ansible.com/ansible/latest/faq.html#how-do-i-generate-crypted-passwords-for-the-user-module


#### Install Passlib password hashing library
```
$ sudo yum install python-pip
$ sudo pip install --upgrade pip
$ sudo pip install passlib
```
#### Generate new password
```
$ python -c "from passlib.hash import sha512_crypt; import getpass; print sha512_crypt.using(rounds=5000).hash(getpass.getpass())"
Password: [Enter password]
$6$fllhdjGxAZSf6jCD$ywmtITXIQqvPgLAOed95UaLopz9FMJODDROtRlc6LIWZIaP0l0G8U4yHavQw9K.BgiquOsLSevNV5JUIcrORQ1
```
#### Copy hashed password to Ansible playbook
```
passwords: $6$sqCxZo4obmZ4LwFc$2AXtD9NkFbj1R11AoR0OOqNQD/NtpqJFIeYe/deMVIMc06wbL2JfrLGXGs1njG/vbW3Am1YHCI6GM5zy4wj/Q0
```



