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

- Create a new `Vagrantfile` for [CentOS v7 (latest)](https://www.centos.org/)

	> vagrant init centos/7

- Check the status of the guest system

	> vagrant status
	Current machine states:
	
	default                   not created (virtualbox)
	...


- Launch the CentOS machine for the first time

	vagrant up

- Enter the CentOS (guest) system

	vagrant ssh

