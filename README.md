# Vagrant - Ubuntu - nginx


Set up a server with the [Ubuntu](https://www.ubuntu.com/) operating system.
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

- Create a new `Vagrantfile` for [Ubuntu Xenial v16](https://www.ubuntu.com/)

	    $ vagrant init ubuntu/xenial64
	    $ ls -l
	    -rw-r--r--  1 tjeerd  staff  3012 Dec 14 10:06 Vagrantfile
	    $

- Start writing a `README.md` which describes the purpose of this project

	    $ echo "# Vagrant - Ubuntu - nginx" > README.md
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
		$


- Launch the Ubuntu machine for the first time  
	Start VirtualBox, so you can see how the _guest operating system_ is created and started.

	    $ vagrant status
		Current machine states:
		
		default                   not created (virtualbox)
		
		The environment has not yet been created. Run `vagrant up` to
		create the environment. If a machine is not created, only the
		default provider will be shown. So if a provider is not listed,
		then the machine is not created for that environment.
		$ vagrant up
		Bringing machine 'default' up with 'virtualbox' provider...
		==> default: Importing base box 'ubuntu/xenial64'...
		==> default: Matching MAC address for NAT networking...
		==> default: Checking if box 'ubuntu/xenial64' is up to date...
		==> default: A newer version of the box 'ubuntu/xenial64' is available! You currently
		==> default: have version '20161122.0.0'. The latest is version '20161213.0.0'. Run
		==> default: `vagrant box update` to update.
		==> default: Setting the name of the VM: vagrant-nginx_default_1481745005258_62301
		==> default: Clearing any previously set network interfaces...
		==> default: Preparing network interfaces based on configuration...
		    default: Adapter 1: nat
		==> default: Forwarding ports...
		    default: 22 (guest) => 2222 (host) (adapter 1)
		==> default: Running 'pre-boot' VM customizations...
		==> default: Booting VM...
		==> default: Waiting for machine to boot. This may take a few minutes...
		    default: SSH address: 127.0.0.1:2222
		    default: SSH username: ubuntu
		    default: SSH auth method: password
		    default: Warning: Remote connection disconnect. Retrying...
		    default: Warning: Remote connection disconnect. Retrying...
		    default: Warning: Remote connection disconnect. Retrying...
		    default: Warning: Authentication failure. Retrying...
		    default: Warning: Remote connection disconnect. Retrying...
		    default: 
		    default: Inserting generated public key within guest...
		    default: Removing insecure key from the guest if it's present...
		    default: Key inserted! Disconnecting and reconnecting using new SSH key...
		==> default: Machine booted and ready!
		==> default: Checking for guest additions in VM...
		    default: The guest additions on this VM do not match the installed version of
		    default: VirtualBox! In most cases this is fine, but in rare cases it can
		    default: prevent things such as shared folders from working properly. If you see
		    default: shared folder errors, please make sure the guest additions within the
		    default: virtual machine match the version of VirtualBox you have installed on
		    default: your host and reload your VM.
		    default: 
		    default: Guest Additions Version: 5.0.24
		    default: VirtualBox Version: 5.1
		==> default: Mounting shared folders...
		    default: /vagrant => /Users/tjeerd/git/vagrant/vagrant-nginx
	    $ vagrant status
		Current machine states:
		
		default                   running (virtualbox)
		
		The VM is running. To stop this VM, you can run `vagrant halt` to
		shut it down forcefully, or you can run `vagrant suspend` to simply
		suspend the virtual machine. In either case, to restart it again,
		simply run `vagrant up`.
		$

- Enter the Ubuntu (guest) system

	    $ vagrant ssh
		Welcome to Ubuntu 16.04.1 LTS (GNU/Linux 4.4.0-47-generic x86_64)
		
		 * Documentation:  https://help.ubuntu.com
		 * Management:     https://landscape.canonical.com
		 * Support:        https://ubuntu.com/advantage
		
		  Get cloud support with Ubuntu Advantage Cloud Guest:
		    http://www.ubuntu.com/business/services/cloud
		
		0 packages can be updated.
		0 updates are security updates.
		
		
		_____________________________________________________________________
		WARNING! Your environment specifies an invalid locale.
		 The unknown environment variables are:
		   LC_CTYPE=UTF-8 LC_ALL=
		 This can affect your user experience significantly, including the
		 ability to manage packages. You may install the locales by running:
		
		   sudo apt-get install language-pack-UTF-8
		     or
		   sudo locale-gen UTF-8
		
		To see all available language packs, run:
		   apt-cache search "^language-pack-[a-z][a-z]$"
		To disable this message for all users, run:
		   sudo touch /var/lib/cloud/instance/locale-check.skip
		_____________________________________________________________________
		
		ubuntu@ubuntu-xenial:~$

- **Guest** Show current working directory on Ubuntu guest system

	    ubuntu@ubuntu-xenial:~$ pwd
		/home/ubuntu
		ubuntu@ubuntu-xenial:~$

- **Guest** Search packages with [APT (Advanced Package Tool)](https://www.google.com/webhp?ion=1&espv=2&ie=UTF-8#q=apt+linux)  
	Show `apt` options  
  
	    $ apt --help
		apt 1.2.15 (amd64)
		Usage: apt [options] command
		
		apt is a commandline package manager and provides commands for
		searching and managing as well as querying information about packages.
		It provides the same functionality as the specialized APT tools,
		like apt-get and apt-cache, but enables options more suitable for
		interactive use by default.
		
		Most used commands:
		  list - list packages based on package names
		  search - search in package descriptions
		  show - show package details
		  install - install packages
		  remove - remove packages
		  autoremove - Remove automatically all unused packages
		  update - update list of available packages
		  upgrade - upgrade the system by installing/upgrading packages
		  full-upgrade - upgrade the system by removing/installing/upgrading packages
		  edit-sources - edit the source information file
		
		See apt(8) for more information about the available commands.
		Configuration options and syntax is detailed in apt.conf(5).
		Information about how to configure sources can be found in sources.list(5).
		Package and version choices can be expressed via apt_preferences(5).
		Security details are available in apt-secure(8).
		                                        This APT has Super Cow Powers.
		ubuntu@ubuntu-xenial:~$ 
	    [vagrant@localhost ~]$ $ apt search nginx
		Sorting... Done
		Full Text Search... Done
		collectd-core/xenial 5.5.1-1build2 amd64
		  statistics collection and monitoring daemon (core system)
		
		coquelicot/xenial 0.9.5-1 all
		  "one-click" file sharing web application with a focus on users' privacy

		...
		
		nginx/xenial-updates,xenial-security 1.10.0-0ubuntu0.16.04.4 all
		  small, powerful, scalable web/proxy server
		
		nginx-common/xenial-updates,xenial-security 1.10.0-0ubuntu0.16.04.4 all
		  small, powerful, scalable web/proxy server - common files
		
		nginx-core/xenial-updates,xenial-security 1.10.0-0ubuntu0.16.04.4 amd64
		  nginx web/proxy server (core version)
		
		nginx-core-dbg/xenial-updates,xenial-security 1.10.0-0ubuntu0.16.04.4 amd64
		  nginx web/proxy server (core version) - debugging symbols
		
		nginx-doc/xenial-updates,xenial-security 1.10.0-0ubuntu0.16.04.4 all
		  small, powerful, scalable web/proxy server - documentation		

		...

		ubuntu@ubuntu-xenial:~$ apt show nginx
		Package: nginx
		Version: 1.10.0-0ubuntu0.16.04.4
		Priority: optional
		Section: web
		Origin: Ubuntu
		Maintainer: Ubuntu Developers <ubuntu-devel-discuss@lists.ubuntu.com>
		Original-Maintainer: Kartik Mistry <kartik@debian.org>
		Bugs: https://bugs.launchpad.net/ubuntu/+filebug
		Installed-Size: 37.9 kB
		Depends: nginx-core (>= 1.10.0-0ubuntu0.16.04.4) | nginx-full (>= 1.10.0-0ubuntu0.16.04.4) | nginx-light (>= 1.10.0-0ubuntu0.16.04.4) | nginx-extras (>= 1.10.0-0ubuntu0.16.04.4), nginx-core (<< 1.10.0-0ubuntu0.16.04.4.1~) | nginx-full (<< 1.10.0-0ubuntu0.16.04.4.1~) | nginx-light (<< 1.10.0-0ubuntu0.16.04.4.1~) | nginx-extras (<< 1.10.0-0ubuntu0.16.04.4.1~)
		Homepage: http://nginx.net
		Supported: 5y
		Download-Size: 3498 B
		APT-Sources: http://archive.ubuntu.com/ubuntu xenial-updates/main amd64 Packages
		Description: small, powerful, scalable web/proxy server
		 Nginx ("engine X") is a high-performance web and reverse proxy server
		 created by Igor Sysoev. It can be used both as a standalone web server
		 and as a proxy to reduce the load on back-end HTTP or mail servers.
		 .
		 This is a dependency package to install either nginx-core (by default),
		 nginx-full, nginx-light, or nginx-extras.
		
		N: There is 1 additional record. Please use the '-a' switch to see it
		ubuntu@ubuntu-xenial:~$ 


- **Guest** Install package [nginx](https://www.nginx.com/)

		ubuntu@ubuntu-xenial:~$ sudo apt install nginx
		Reading package lists... Done
		Building dependency tree       
		Reading state information... Done
		The following additional packages will be installed:
		  fontconfig-config fonts-dejavu-core libfontconfig1 libgd3 libjbig0 libjpeg-turbo8 libjpeg8 libtiff5 libvpx3 libxpm4 libxslt1.1 nginx-common nginx-core
		Suggested packages:
		  libgd-tools fcgiwrap nginx-doc ssl-cert
		The following NEW packages will be installed:
		  fontconfig-config fonts-dejavu-core libfontconfig1 libgd3 libjbig0 libjpeg-turbo8 libjpeg8 libtiff5 libvpx3 libxpm4 libxslt1.1 nginx nginx-common nginx-core
		0 upgraded, 14 newly installed, 0 to remove and 0 not upgraded.
		Need to get 2995 kB of archives.
		After this operation, 9794 kB of additional disk space will be used.
		Do you want to continue? [Y/n] y
		Get:1 http://archive.ubuntu.com/ubuntu xenial/main amd64 libjpeg-turbo8 amd64 1.4.2-0ubuntu3 [111 kB]
		Get:2 http://archive.ubuntu.com/ubuntu xenial/main amd64 libxpm4 amd64 1:3.5.11-1 [33.1 kB]
		Get:3 http://archive.ubuntu.com/ubuntu xenial/main amd64 libjbig0 amd64 2.1-3.1 [26.6 kB]
		Get:4 http://archive.ubuntu.com/ubuntu xenial/main amd64 fonts-dejavu-core all 2.35-1 [1039 kB]
		Get:5 http://archive.ubuntu.com/ubuntu xenial-updates/main amd64 fontconfig-config all 2.11.94-0ubuntu1.1 [49.9 kB]
		Get:6 http://archive.ubuntu.com/ubuntu xenial-updates/main amd64 libfontconfig1 amd64 2.11.94-0ubuntu1.1 [131 kB]
		Get:7 http://archive.ubuntu.com/ubuntu xenial/main amd64 libjpeg8 amd64 8c-2ubuntu8 [2194 B]
		Get:8 http://archive.ubuntu.com/ubuntu xenial/main amd64 libtiff5 amd64 4.0.6-1 [144 kB]                                                                                      
		Get:9 http://archive.ubuntu.com/ubuntu xenial/main amd64 libvpx3 amd64 1.5.0-2ubuntu1 [732 kB]                                                                                
		Get:10 http://archive.ubuntu.com/ubuntu xenial-updates/main amd64 libgd3 amd64 2.1.1-4ubuntu0.16.04.5 [125 kB]                                                                
		Get:11 http://archive.ubuntu.com/ubuntu xenial/main amd64 libxslt1.1 amd64 1.1.28-2.1 [145 kB]                                                                                
		Get:12 http://archive.ubuntu.com/ubuntu xenial-updates/main amd64 nginx-common all 1.10.0-0ubuntu0.16.04.4 [26.6 kB]                                                          
		Get:13 http://archive.ubuntu.com/ubuntu xenial-updates/main amd64 nginx-core amd64 1.10.0-0ubuntu0.16.04.4 [428 kB]                                                           
		Get:14 http://archive.ubuntu.com/ubuntu xenial-updates/main amd64 nginx all 1.10.0-0ubuntu0.16.04.4 [3498 B]                                                                  
		Fetched 2995 kB in 7s (401 kB/s)                                                                                                                                              
		perl: warning: Setting locale failed.
		perl: warning: Please check that your locale settings:
			LANGUAGE = (unset),
			LC_ALL = (unset),
			LC_CTYPE = "UTF-8",
			LANG = "en_US.UTF-8"
		    are supported and installed on your system.
		perl: warning: Falling back to a fallback locale ("en_US.UTF-8").
		locale: Cannot set LC_CTYPE to default locale: No such file or directory
		locale: Cannot set LC_ALL to default locale: No such file or directory
		Preconfiguring packages ...
		Selecting previously unselected package libjpeg-turbo8:amd64.
		(Reading database ... 53687 files and directories currently installed.)
		Preparing to unpack .../libjpeg-turbo8_1.4.2-0ubuntu3_amd64.deb ...
		Unpacking libjpeg-turbo8:amd64 (1.4.2-0ubuntu3) ...
		Selecting previously unselected package libxpm4:amd64.
		
		...
		
		Setting up nginx-common (1.10.0-0ubuntu0.16.04.4) ...
		locale: Cannot set LC_CTYPE to default locale: No such file or directory
		locale: Cannot set LC_ALL to default locale: No such file or directory
		Setting up nginx-core (1.10.0-0ubuntu0.16.04.4) ...
		Setting up nginx (1.10.0-0ubuntu0.16.04.4) ...
		Processing triggers for libc-bin (2.23-0ubuntu4) ...
		Processing triggers for systemd (229-4ubuntu12) ...
		Processing triggers for ureadahead (0.100.0-19) ...
		Processing triggers for ufw (0.35-0ubuntu2) ...
		ubuntu@ubuntu-xenial:~$
	
	**Question:** What will happen if you install again the same package? Try it out!

- **Guest** Check that the nginx service is running

		ubuntu@ubuntu-xenial:~$ service nginx status
		● nginx.service - A high performance web server and a reverse proxy server
		   Loaded: loaded (/lib/systemd/system/nginx.service; enabled; vendor preset: enabled)
		   Active: active (running) since Wed 2016-12-14 20:15:20 UTC; 2min 30s ago
		 Main PID: 11862 (nginx)
		   CGroup: /system.slice/nginx.service
		           ├─11862 nginx: master process /usr/sbin/nginx -g daemon on; master_process on
		           ├─11863 nginx: worker process                           
		           └─11864 nginx: worker process                           
		
		Dec 14 20:15:20 ubuntu-xenial systemd[1]: Starting A high performance web server and a reverse proxy server...
		Dec 14 20:15:20 ubuntu-xenial systemd[1]: nginx.service: Failed to read PID from file /run/nginx.pid: Invalid argument
		Dec 14 20:15:20 ubuntu-xenial systemd[1]: Started A high performance web server and a reverse proxy server.
		ubuntu@ubuntu-xenial:~$
	
	Use curl to see the content of the main page of the nginx web server
	
		ubuntu@ubuntu-xenial:~$ curl http://localhost:80
		<!DOCTYPE html>
		<html>
		<head>
		<title>Welcome to nginx!</title>
		<style>
		    body {
		        width: 35em;
		        margin: 0 auto;
		        font-family: Tahoma, Verdana, Arial, sans-serif;
		    }
		</style>
		</head>
		<body>
		<h1>Welcome to nginx!</h1>
		<p>If you see this page, the nginx web server is successfully installed and
		working. Further configuration is required.</p>
		
		<p>For online documentation and support please refer to
		<a href="http://nginx.org/">nginx.org</a>.<br/>
		Commercial support is available at
		<a href="http://nginx.com/">nginx.com</a>.</p>
		
		<p><em>Thank you for using nginx.</em></p>
		</body>
		</html>
		ubuntu@ubuntu-xenial:~$ 

- **Guest** Lookup which ip-address is assigned to the (VirtualBox) nic's (Network Interface Card)

		ubuntu@ubuntu-xenial:~$ ifconfig
		enp0s3    Link encap:Ethernet  HWaddr 02:c2:b4:4c:cc:47  
		          inet addr:10.0.2.15  Bcast:10.0.2.255  Mask:255.255.255.0
		          inet6 addr: fe80::c2:b4ff:fe4c:cc47/64 Scope:Link
		          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
		          RX packets:5348 errors:0 dropped:0 overruns:0 frame:0
		          TX packets:2894 errors:0 dropped:0 overruns:0 carrier:0
		          collisions:0 txqueuelen:1000 
		          RX bytes:3362579 (3.3 MB)  TX bytes:250899 (250.8 KB)
		
		lo        Link encap:Local Loopback  
		          inet addr:127.0.0.1  Mask:255.0.0.0
		          inet6 addr: ::1/128 Scope:Host
		          UP LOOPBACK RUNNING  MTU:65536  Metric:1
		          RX packets:14 errors:0 dropped:0 overruns:0 frame:0
		          TX packets:14 errors:0 dropped:0 overruns:0 carrier:0
		          collisions:0 txqueuelen:1 
		          RX bytes:1732 (1.7 KB)  TX bytes:1732 (1.7 KB)
		
		ubuntu@ubuntu-xenial:~$
	
	The nic `lo` is the loopback / localhost / 127.0.0.1 one. Check the ip-address (here `10.0.2.15`) of the other nic.
	
	**Question:** How is the other nic configured? Look it up in VirtualBox.

	Leave the guest-os, and stop the guest-os.
	
		ubuntu@ubuntu-xenial:~$ exit
		logout
		Connection to 127.0.0.1 closed.
		$ vagrant halt
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
		
	Start Ubuntu again.
	
		$ vagrant up
		Bringing machine 'default' up with 'virtualbox' provider...
		==> default: Checking if box 'ubuntu/xenial64' is up to date...
		==> default: A newer version of the box 'ubuntu/xenial64' is available! You currently
		==> default: have version '20161122.0.0'. The latest is version '20161213.0.0'. Run
		==> default: `vagrant box update` to update.
		==> default: Clearing any previously set forwarded ports...
		==> default: Clearing any previously set network interfaces...
		==> default: Preparing network interfaces based on configuration...
		    default: Adapter 1: nat
		==> default: Forwarding ports...
		    default: 80 (guest) => 8080 (host) (adapter 1)
		    default: 22 (guest) => 2222 (host) (adapter 1)
		==> default: Running 'pre-boot' VM customizations...
		==> default: Booting VM...
		==> default: Waiting for machine to boot. This may take a few minutes...
		    default: SSH address: 127.0.0.1:2222
		    default: SSH username: ubuntu
		    default: SSH auth method: password
		    default: Warning: Remote connection disconnect. Retrying...
		    default: Warning: Remote connection disconnect. Retrying...
		    default: Warning: Remote connection disconnect. Retrying...
		    default: Warning: Remote connection disconnect. Retrying...
		==> default: Machine booted and ready!
		==> default: Checking for guest additions in VM...
		    default: The guest additions on this VM do not match the installed version of
		    default: VirtualBox! In most cases this is fine, but in rare cases it can
		    default: prevent things such as shared folders from working properly. If you see
		    default: shared folder errors, please make sure the guest additions within the
		    default: virtual machine match the version of VirtualBox you have installed on
		    default: your host and reload your VM.
		    default: 
		    default: Guest Additions Version: 5.0.24
		    default: VirtualBox Version: 5.1
		==> default: Mounting shared folders...
		    default: /vagrant => /Users/tjeerd/git/vagrant/vagrant-nginx
		==> default: Machine already provisioned. Run `vagrant provision` or use the `--provision`
		==> default: flag to force provisioning. Provisioners marked to run always will still run.
		$
	
	Check if the port forwarding works.
	
		$ curl localhost:8080
		<!DOCTYPE html>
		<html>
		<head>
		<title>Welcome to nginx!</title>
		<style>
		    body {
		        width: 35em;
		        margin: 0 auto;
		        font-family: Tahoma, Verdana, Arial, sans-serif;
		    }
		</style>
		</head>
		<body>
		<h1>Welcome to nginx!</h1>
		<p>If you see this page, the nginx web server is successfully installed and
		working. Further configuration is required.</p>
		
		<p>For online documentation and support please refer to
		<a href="http://nginx.org/">nginx.org</a>.<br/>
		Commercial support is available at
		<a href="http://nginx.com/">nginx.com</a>.</p>
		
		<p><em>Thank you for using nginx.</em></p>
		</body>
		</html>
		$
	
	Double check! Open a browser and go to [http://localhost:8080/](http://localhost:8080/)
	
	It should show the default opening page.
	
	<img  src="https://raw.githubusercontent.com/verhagen/vagrant-nginx/master/images/nginx-welcome-00.jpg" />
	
- Stop the Ubuntu (guest) system

		$ vagrant status
		Current machine states:
		
		default                   running (virtualbox)
		
		The VM is running. To stop this VM, you can run `vagrant halt` to
		shut it down forcefully, or you can run `vagrant suspend` to simply
		suspend the virtual machine. In either case, to restart it again,
		simply run `vagrant up`.
		$ vagrant halt
		==> default: Attempting graceful shutdown of VM...
		$ vagrant status
		Current machine states:
		
		default                   poweroff (virtualbox)
		
		The VM is powered off. To restart the VM, simply run `vagrant up`
		$

	The guest system is now stopped, see also VirualBox. To start it again use `vagrant up` again.
	
	**Question:** When `vagrant up` is now used. Is nginx then still installed and running?
	Try it out to check it!

- Remove the Ubuntu system completely form VirtualBox

		$ vagrant destroy
		    default: Are you sure you want to destroy the 'default' VM? [y/N] y
		==> default: Destroying VM and associated drives...
		$

	The guest system is removed now, see also VirualBox.

	**Question:** When `vagrant up` is now used _again_. Is nginx still
	installed and running? Try it out to check it!

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

