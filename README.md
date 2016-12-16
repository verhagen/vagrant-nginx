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
	
	**Question:** When `vagrant up` is now used. Is the Java JDK then still installed?
	Try it out to check it!

- Remove the CentOS system completely form VirtualBox

		$ vagrant destroy
		    default: Are you sure you want to destroy the 'default' VM? [y/N] y
		==> default: Destroying VM and associated drives...
		$

	The guest system is removed now, see also VirualBox.

	**Question:** When `vagrant up` is now used _again_. Is the Java JDK then still
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

## Add nginx

the pacakge nginx is not directly support in CentOS. But adding the
[Extra Packages for Enterprise Linux (EPEL)](https://fedoraproject.org/wiki/EPEL) repository,
gives access to nginx package as well.
See also [How To Install Nginx on CentOS 7](https://www.digitalocean.com/community/tutorials/how-to-install-nginx-on-centos-7).

- Launch and enter CentOS

	    $ vagrant up
	    $ vagrant ssh

- Add the Extra Packages for Enterprise Linux (EPEL)

		$ sudo yum install epel-release

- Search in yum for nginx

		[vagrant@localhost ~]$ yum search nginx
		Failed to set locale, defaulting to C
		Loaded plugins: fastestmirror
		epel/x86_64/metalink                                                                                 |  24 kB  00:00:00     
		epel                                                                                                 | 4.3 kB  00:00:00     
		(1/3): epel/x86_64/updateinfo                                                                        | 691 kB  00:00:00     
		(2/3): epel/x86_64/group_gz                                                                          | 170 kB  00:00:00     
		(3/3): epel/x86_64/primary_db                                                                        | 4.4 MB  00:00:01     
		Loading mirror speeds from cached hostfile
		 * base: mirror.i3d.net
		 * epel: mirror.serverbeheren.nl
		 * extras: centos.mirror.transip.nl
		 * updates: mirror.i3d.net
		=============================================== N/S matched: nginx ====================================================
		collectd-nginx.x86_64 : Nginx plugin for collectd
		munin-nginx.noarch : Network-wide graphing framework (cgi files for nginx)
		nginx-all-modules.noarch : A meta package that installs all available Nginx modules
		nginx-filesystem.noarch : The basic directory layout for the Nginx server
		nginx-mod-http-geoip.x86_64 : Nginx HTTP geoip module
		nginx-mod-http-image-filter.x86_64 : Nginx HTTP image filter module
		nginx-mod-http-perl.x86_64 : Nginx HTTP perl module
		nginx-mod-http-xslt-filter.x86_64 : Nginx XSLT module
		nginx-mod-mail.x86_64 : Nginx mail modules
		nginx-mod-stream.x86_64 : Nginx stream modules
		owncloud-nginx.noarch : Nginx integration for ownCloud
		pcp-pmda-nginx.x86_64 : Performance Co-Pilot (PCP) metrics for the Nginx Webserver
		nginx.x86_64 : A high performance web server and reverse proxy server
		
		  Name and summary matches only, use "search all" for everything.
		[vagrant@localhost ~]$

- Add nginx

		$ sudo yum install -y nginx

- Check if nginx is running

		[vagrant@localhost ~]$ systemctl status nginx
		● nginx.service - The nginx HTTP and reverse proxy server
		   Loaded: loaded (/usr/lib/systemd/system/nginx.service; disabled; vendor preset: disabled)
		   Active: inactive (dead)
		[vagrant@localhost ~]$

- Start nginx and check status again

		[vagrant@localhost ~]$ sudo systemctl start nginx
		[vagrant@localhost ~]$ systemctl status nginx
		● nginx.service - The nginx HTTP and reverse proxy server
		   Loaded: loaded (/usr/lib/systemd/system/nginx.service; disabled; vendor preset: disabled)
		   Active: active (running) since Fri 2016-12-16 21:49:38 UTC; 4s ago
		  Process: 11829 ExecStart=/usr/sbin/nginx (code=exited, status=0/SUCCESS)
		  Process: 11827 ExecStartPre=/usr/sbin/nginx -t (code=exited, status=0/SUCCESS)
		  Process: 11825 ExecStartPre=/usr/bin/rm -f /run/nginx.pid (code=exited, status=0/SUCCESS)
		 Main PID: 11832 (nginx)
		   CGroup: /system.slice/nginx.service
		           ├─11832 nginx: master process /usr/sbin/nginx
		           └─11833 nginx: worker process
		[vagrant@localhost ~]$

	Check that nginx is up
	
		[vagrant@localhost ~]$ curl http://localhost/
		<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.1//EN" "http://www.w3.org/TR/xhtml11/DTD/xhtml11.dtd">
		
		<html xmlns="http://www.w3.org/1999/xhtml" xml:lang="en">
		    <head>
		        <title>Test Page for the Nginx HTTP Server on Fedora</title>
		        
		        ...
		        
		                <a href="http://fedoraproject.org/"><img 
		                    src="poweredby.png" 
		                    alt="[ Powered by Fedora ]" 
		                    width="88" height="31" /></a>
		            </div>
		        </div>
		    </body>
		</html>
		[vagrant@localhost ~]$

- **Guest** Stop the guest-os

	Leave the guest-os and stop the guest-os

		[vagrant@localhost ~]$ exit
		logout
		Connection to 127.0.0.1 closed.
		Tjeerds-MacBook-Pro:vagrant-nginx tjeerd$ vagrant halt
		==> default: Attempting graceful shutdown of VM...
		$

- Forward the guest port `80` to the host `8080`
	
	Edit the file `Vagrantfile` and remove the hash `#`, from the line:
	
		config.vm.network "forwarded_port", guest: 80, host: 8080
	
	Make sure there is nothing already running on that port `8080`, like Tomcat, Jetty or other things.
	Check it with `curl`, it should fail to connect.

		$ curl localhost:8080
		curl: (7) Failed to connect to localhost port 8080: Connection refused
		$
		
	Start CentOS again.
	
		$ vagrant up
		Bringing machine 'default' up with 'virtualbox' provider...
		==> default: Checking if box 'centos/7' is up to date...
		==> default: A newer version of the box 'centos/7' is available! You currently
		==> default: have version '1610.01'. The latest is version '1611.01'. Run
		==> default: `vagrant box update` to update.
		==> default: Clearing any previously set forwarded ports...
		==> default: Fixed port collision for 22 => 2222. Now on port 2200.
		==> default: Clearing any previously set network interfaces...
		==> default: Preparing network interfaces based on configuration...
		    default: Adapter 1: nat
		==> default: Forwarding ports...
		    default: 80 (guest) => 8080 (host) (adapter 1)
		    default: 22 (guest) => 2200 (host) (adapter 1)
		==> default: Booting VM...
		==> default: Waiting for machine to boot. This may take a few minutes...
		    default: SSH address: 127.0.0.1:2200
		    default: SSH username: vagrant
		    default: SSH auth method: private key
		==> default: Machine booted and ready!
		==> default: Checking for guest additions in VM...
		    default: No guest additions were detected on the base box for this VM! Guest
		    default: additions are required for forwarded ports, shared folders, host only
		    default: networking, and more. If SSH fails on this machine, please install
		    default: the guest additions and repackage the box to continue.
		    default: 
		    default: This is not an error message; everything may continue to work properly,
		    default: in which case you may ignore this message.
		==> default: Rsyncing folder: /Users/tjeerd/git/vagrant/vagrant-nginx/ => /vagrant
		==> default: Machine already provisioned. Run `vagrant provision` or use the `--provision`
		==> default: flag to force provisioning. Provisioners marked to run always will still run.
		$

	Check if the port forwarding works.
	
		$ curl localhost:8080
	
	Double check! Open a browser and go to [http://localhost:8080/](http://localhost:8080/) 	
	
	It should show the default opening page.
	
	<img  src="https://raw.githubusercontent.com/verhagen/vagrant-nginx/master/images/nginx-welcome-00.jpg" />

