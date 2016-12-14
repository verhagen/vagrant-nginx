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

	    $ mkdir -p ~/git/vagrant/vagrant-nginx
	    $ cd ~/git/vagrant/vagrant-nginx
	    $

- Create a new `Vagrantfile` for [CentOS v7 (latest)](https://www.centos.org/)

	    $ vagrant init centos/7
	    $ ls -l
	    -rw-r--r--  1 tjeerd  staff  3012 Dec 14 10:06 Vagrantfile
	    $

- Start writing a `README.md` which describes the purpose of this project

	    $ echo "# Vagrant - CentOS - nginx" > README.md
	    $ ls -l
	    -rw-r--r--@  1 tjeerd  staff  1018 Dec 14 10:27 README.md
	    -rw-r--r--   1 tjeerd  staff  3012 Dec 14 10:06 Vagrantfile
	    $

- Initialize / create a git repository

	    $ git init
	    $ git status
	    @TODO
	    $

- Add the current files `README.md` and `Vagrantfile` to git stash (index) area

	    $ git add *
	    $ git status
	    @TODO

- Commit the stashed files to the (default _master_) branch

	    $ git commit -m "Start new project"
	    $ git status
	    @TODO
	    $

- Check the status of the guest system

	    $ vagrant status
	    Current machine states:
	    
	    default                   not created (virtualbox)
	    ...
		[vagrant@localhost ~]$


- Launch the CentOS machine for the first time  
	Start VirtualBox, so you can see how the _guest operating system_ is created and started.

	    $ vagrant up
	    $ vagrant status
	    Current machine states:
	    
	    default                   running (virtualbox)
	    ...
		[vagrant@localhost ~]$

- Enter the CentOS (guest) system

	    $ vagrant ssh
	    -bash: warning: setlocale: LC_CTYPE: cannot change locale (UTF-8): No such file or directory
	    [vagrant@localhost ~]$

- **Guest** Show current working directory on CentOS guest system

	    [vagrant@localhost ~]$ pwd
	    /home/vagrant
		[vagrant@localhost ~]$

- **Guest** Search packages with [YUM (Yellowdog Updater Modified)](https://www.google.com/webhp?ion=1&espv=2&ie=UTF-8#q=yum+linux)  
	Show `yum` options  
  
	    [vagrant@localhost ~]$ yum --help

	    [vagrant@localhost ~]$ yum search java
	    [vagrant@localhost ~]$ yum search java-1.8
	    [vagrant@localhost ~]$


- **Guest** Install package Java Development Kit 1.8.0 [(OpenJDK)](http://openjdk.java.net/)

	    [vagrant@localhost ~]$ sudo yum install java-1.8.0-openjdk-devel
	    
	    [vagrant@localhost ~]$ java -version
	    openjdk version "1.8.0_111"
	    OpenJDK Runtime Environment (build 1.8.0_111-b15)
	    OpenJDK 64-Bit Server VM (build 25.111-b15, mixed mode)
	    [vagrant@localhost ~]$

- **Guest** Leave the CentOS (guest) system

	    [vagrant@localhost ~]$ exit
		logout
		Connection to 127.0.0.1 closed.
		$ 

- Stop the CentOS (guest) system

		$ vagrant status
		Current machine states:
		
		default                   running (virtualbox)
		
		The VM is running. To stop this VM, you can run `vagrant halt` to
		shut it down forcefully, or you can run `vagrant suspend` to simply
		suspend the virtual machine. In either case, to restart it again,
		simply run `vagrant up`.
		$ vagrant halt
		==> default: Attempting graceful shutdown of VM...
		$ vagrant halt
		==> default: Attempting graceful shutdown of VM...
		Tjeerds-MacBook-Pro:vagrant-nginx tjeerd$ vagrant status
		Current machine states:
		
		default                   poweroff (virtualbox)
		
		The VM is powered off. To restart the VM, simply run `vagrant up`
		$

	The guest system is now stopped, see also VirualBox. To start it again use `vagrant up` again.
	
	Question: When `vagrant up` is now used. Is the Java JDK then still installed?
	Try it out to check it!

- Remove the CentOS system completely form VirtualBox

		$ vagrant destroy
		    default: Are you sure you want to destroy the 'default' VM? [y/N] y
		==> default: Destroying VM and associated drives...
		$

	The guest system is removed now, see also VirualBox.

	Question: When `vagrant up` is now used _again_. Is the Java JDK then still
	installed? Try it out to check it!

- Check if there are git changes 

	    $ git status
	    On branch master
	    Untracked files:
	      (use "git add <file$..." to include in what will be committed)
	    
	        .vagrant/
	    
	    nothing added to commit but untracked files present (use "git add" to track)  
		$
	
	This directory `.vagrant` should not be added to git repository. So add it to the
	`.gitignore` file.

	    $ echo .vagrant/ >> .gitignore
		$
	    
	Show the current content of the file `.gitignore`
	    
	    $ cat .gitignore 
		.project
		.vagrant/
	    $ git status
	    On branch master
	    Changes not staged for commit:
	      (use "git add <file>..." to update what will be committed)
	      (use "git checkout -- <file>..." to discard changes in working directory)
	
	        modified:   .gitignore
	
	    no changes added to commit (use "git add" and/or "git commit -a")
		$

	Add the updated `.gitignore` to the git stash area and commit the stahed change(s)
	    
	    $ git add .gitignore
	    $ git commit -m "Adds directory .vagrant"
	    [master 8f2304c] Adds directory .vagrant
	     1 file changed, 1 insertion(+)
		$

