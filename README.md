# Vagrant - CentOS - nginx


Set up a server with the [CentOS](https://www.centos.org/) operating system.
Install [nginx](https://www.nginx.com/).
Add some static content.


## Prerequisites

Make sure the following tools are installed on your (host) system:

- Install [VirtualBox](https://www.virtualbox.org/) and Extension Pack
- Install [Vagrant](https://www.vagrantup.com/)


## Action Plan

- Create a new directory for the project

	> mkdir -p ~/git/vagrant/vagrant-nginx
	> cd ~/git/vagrant/vagrant-nginx

- Create a new `Vagrantfile` for [CentOS v7 (latest)](https://www.centos.org/)

	> vagrant init centos/7
	> ls -l
	-rw-r--r--  1 tjeerd  staff  3012 Dec 14 10:06 Vagrantfile

- Start writing a `README.md` which describes the purpose of this project

    > echo "# Vagrant - CentOS - nginx" > README.md
    > ls -l
    -rw-r--r--@  1 tjeerd  staff  1018 Dec 14 10:27 README.md
	-rw-r--r--   1 tjeerd  staff  3012 Dec 14 10:06 Vagrantfile

- Initialize as git project

    > git init
    > git status
    @TODO

- Add current files to git repository

    > git add *
    > git status
    @TODO
    > git commit -m "Start new project"
    > git status
    @TODO

- Check the status of the guest system

	> vagrant status
	Current machine states:
	
	default                   not created (virtualbox)
	...


- Launch the CentOS machine for the first time

	> vagrant up
	> vagrant status
	Current machine states:
	
	default                   running (virtualbox)
	...

- Enter the CentOS (guest) system

	vagrant ssh


- Check changes 

