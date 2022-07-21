---
layout: page
title: "UNIX"
permalink: /terminal/
---

# Terminal Commands
A cheat sheet for working in a UNIX terminal.

* [Common Commands](#common-commands)
* [Apps](#apps)
* [Problems](#got-a-problem)


## Common Commands
* [Bash functions](#bash-functions)
* [Terminal Windows](#terminal-windows)
* [File Operations](#file-operation)

### Bash Functions
Change prompt to "username@hostname:cwd \$"

~~~
export PS1="\[\033[36m\]\u\[\033[m\]@\[\033[32m\]\h:\[\033[33;1m\]\w\[\033[m\]\$ "
~~~

Enable command line colors

~~~
export CLICOLOR=1
~~~

Define colors for the 'ls'

~~~
export LSCOLORS=ExFxBxDxCxegedabagacad
~~~

Short-cut

* G: colorizes output
* h: makes sizes human readable
* F: throws a / after a directory

~~~
alias ls='ls -GFh'
~~~


### Terminal windows
Update packages:
`sudo apt update`
`sudo apt upgrade`


Freeze windows `ctrl+s` and release it `ctrl+q`

turn off scroll through history: `tput rmcup`

New windows:

	Ctrl+Shift+N

Set up initial environment:
https://www.ibm.com/developerworks/linux/library/l-tip-prompt/

Run a script containing "cd"

	. name.sh

To download new fonts:sudo apt-get install ttf-mscorefonts-installer
    Fix the download failed problem: 1.Alt+F2. 2.Type "software-properties.gtk" 3.Click in and select the "Download from" option as "Main server".
    
To change user password into anything:sudo passwd user:

    delete passwd: passwd -d username

Drop to a console: 

	Ctrl+Alt+F1; Crtl+Alt+F7 to go back.

Adjust username: 

	usermod

Process management:top; 

	Ctrl+L to search;

End a process: 

	xkill; 
	killall process_name

End a process precisely:

1. Locate PID#: 

		ps u
	
3.  Kill:

		kill PID#
		kill -9 PID# (kill a process immediately)
	
1. Kill in the top:

		top, k, PID#, 9 (kill a process in top)

Open the current folder and select the file: 

		nautilus file_name

Open a file A under current directory in a new window:

	gnome-open A (Tab to fill the name)
	xdg-open A

Folder Navigation:

    cd A (Change to a directory named A); 
    cd .. (move up one folder); 
    cd - (get back);
    ls         (list files); 
    ls -d -- */ (list all the directories in current directory)
    ls -lrth (show dates of diles)
    ls -al (show all link)

Link a file (shortcut)
	 
	 ln -s <target> <file for calling the target> 

We can see where the symbolic is linked to using `ls -la `



Open setting: 

	unity-control-center

Shutdown the system via any of the followings:

	poweroff;
	shutdown --help (Information of shutdown); 
	shutdown 5 (shutdown after 5 minutes); 
	reboot (restart)

Search a pattern in a file: `grep pattern file_name`

search a tab: `grep -P '\t' ./*`

view running processes:

	gnome-system-monitor
Show installed apps:

	apt list --installed
Download Website:

	wget --mirror -p --convert-links -P ~/Desktop/C/Books/ http://www.ee.surrey.ac.uk/Teaching/Unix/
	
	--no-parent - do not download files form folders below given root folder (folder1/folder/ in our example; files from /folder1 are not going to be transferred).

Intallation Global vs. local

- Global directory: `/usr/local/bin/`
- local directory: `$HOME/`

### Deal with text
`cat <text_file>` Concatenates files And print on the stand output

Print output (https://askubuntu.com/questions/420981/how-do-i-save-terminal-output-to-a-file)
	
	<executable> > <.txt> //rediret output
	<executable> 2> <.txt> //rediret stdeer
	<executable> &> <.txt> //redirect stdeer & output
	<executable> >> <.txt> //append output
	<executable> &>> <.txt> //append stdeer & output
	<executable> 2>&1 <.txt> //append stdeer & output and display them

### Desktop icons
Remove trash can desktop icon in ubuntu 20.04 [link](https://tipsonubuntu.com/2020/04/06/move-trash-dock-panel-ubuntu-20-04/):
	
	gsettings set org.gnome.shell.extensions.desktop-icons show-trash false

### Get connected
	ssh -X account@server
Copy file to the school:

	ssh-copy-id -i ~/.ssh/id_rsa.pub account@server
Copy file again:

	scp <file> <username>@<IP address or hostname>:<Destination>

### File operation
`ls -alF` shows detail of files in the current folder.

`du -a -h` checks the size of files in terminal:

`rm <file>` deletes a file (permanently): 

Delete an empty folder

	rmdir folder

Delete a non-empty folder:

	rm -rf folder

Copy a file (-b means backup):

	cp -b [file name] [location]

Rename a file:

	mv [old name] [new name]

Move a file:

	mv file_name location

Create and edit a text file (in nano):

	sudo nano /location

Use `chmod` to chnage permission of a file with a permission code:

0777: read & write & execute to everyone  
755: read & execute to the owner


---
## Apps
* [tar](#tar)
* [pdftk](#pdftk)
* [tmux](#tmux)
* [make](#make)
* [jekyll](#jekyll)
* [Netcat](#netcat)
* [nethogs](#nethogd)
* [Dig](#dig)
* [Home Brew](#brew)
* [xmllint](#xmllint)

### App Management

A not reliable way

Install ZOOM via `sudo snap install zoom-client`
Remove it  via `sudo snap remove zoom-client`

should do it via:
```
sudo apt-get remove zoom
wget http://zoom.us/client/latest/zoom_amd64.deb
sudo apt install ./zoom_amd64.deb
rm zoom_amd64.deb
```


### Installed Tools
ipython/ idle3/ otave/ jupyter notebook/ putty/ dconf/ gnome-tweaks/pdftk/lutris
	
### echo
Apply `/` in the printout

`echo -e "\na` will produce

```

a
```

### pdftk

Get all pdf in one:

	pdftk * pdf cat output ALL.pdf

Two slide in one page:
	
	pdfjam Page1.pdf Page2.pdf --nup 2x1 --landscape --outfile Page1+2.pdf

Rearrange Pdf layout (column x row)
	
	pdfnup --nup 2x1 mypdf.pdf

### tmux

#### Console
Call up special command throuh `Ctrl+b + <command>`:

enable scrolling: `<command> = [`
next windows: `<command> = )`

#### Session Management
`tmux list-sessions` shows sessions.

`tmux a` attaches the last session
`tmux a -t <session #/name>` attaches the session in the list.

`tmux kill-session -t <name of sessions>` to end one session. 

`tmux kill-server` or `pkill -f tmux` to kill all tmux sessions

### Tar
Extract a a `.tar.gz` file
	
	tar -zxvf file.tar.gz
	tar -xvf file.tar

### Make
`etc/Makefile.arch` has some alias that can be directly used that vary according to operation system.

- `*.so` is a dynamic library

Some grammar for Makefile:

For given input `A:B`, `$@` calls `A` and `$^` calls `B`.

### Jekyll
Activate webpage in the local computer:

	bundle exec jekyll serve

Go to `http://localhost:4000` to visit it from the browser: 

### Netcat
A tool to check network connection
`nc -c <url> <port>`
gives the connection infomation

### nethogs
A tool to check network usage
`sudo nethogs $device`

### Dig
A tool for network trouble shooting

Run a general diagnosis:
`dig smtp.office365.com`

### Brew
See what homebrew has installed in your computer
`brew list`

### xmllint
See what's wrong with your xml file:
`xmllint --noout <*.xml>`

---
## Projects
* [Formating a flash drive](#formating-a-flash-drive)
* [To be a Wlan server](#to-be-a-wlan-server)
* [To be a VPN server](#to-be-a-VPN-server)
* [SSH keyparis](#set-up-ssh-keypairs-auto-log-in)


### Formating a flash drive
Remove bad blocks:

		Ooohu@Ooohu:~$ lsblk
		NAME   MAJ:MIN RM   SIZE RO TYPE MOUNTPOINT
		sda      8:0    0 111.8G  0 disk 
		├─sda1   8:1    0 107.8G  0 part /
		└─sda2   8:2    0     4G  0 part [SWAP]
		sdb      8:16   1  28.9G  0 disk 
		└─sdb1   8:17   1  28.9G  0 part 
		Ooohu@Ooohu:~$ sudo fsck /dev/sdb1

Change it to the NTFS:

		sudo mkfs.ntfs -f /dev/name

### To be a Wlan server
Install Samba: 

		sudo apt-get install samba

Set up password for yourself (Ooohu) for log in.

		sudo smbpasswd -a Ooohu

Configurate
		
		sudo vim /etc/samba/smb.conf

Add the following lines:

		[NAME]
		comment = A Ubuntu server
		path = ~/Public/ 
		read only = no
		guest ok = yes

AND manually right click the ~/Public/ file, and open it to guest user
in "Local Network Share"

Check local ip for connection (in the wlan0 section):
	
		ifconfig

### To be a VPN server
Tutorial from https://linuxconfig.org/openvpn-setup-on-ubuntu-18-04-bionic-beaver-linux

- Install OpenVPN in phone; install easy-rsa and openvpn in Ubuntu.
	
		$sudo apt-get update && sudo apt-get install openvpn easy-rsa

-
Create a working directory (via easy-rsa package) and move in to this
directory:
		
	$ make-cadir certificates && cd certificates

1. Adjust variables in the certificate/vas file. From
	
		export KEY_CONFIG=`$EASY_RSA/whichopensslcnf $EASY_RSA`
		
		export KEY_COUNTRY="US"
		export KEY_PROVINCE="CA"
		export KEY_CITY="SanFrancisco"
		export KEY_ORG="Fort-Funston"
		export KEY_EMAIL="me@myhost.mydomain"
		export KEY_OU="MyOrganizationalUnit"
	to
	
		export KEY_CONFIG=`$EASY_RSA/openssl-1.0.0.cnf`
		
		export KEY_COUNTRY="US"
		export KEY_PROVINCE="NY"
		export KEY_CITY="NYC"
		export KEY_ORG="CHN"
		export KEY_EMAIL="1@2.com"
		export KEY_OU="ME"
	
	then "source" the variables after finished editing:
	
		$ source vars

2. Generate the CA (certificate authority) (ca.crt). Follow the instruction and 
	use "enters" to answer questions.
	
		$ ./clean-all && ./build-ca

3. Generate the certificate (serve.crt) and key (server.key).  
Follow the instruction and use "enters" to answer questions.
	
		$ ./build-key-server server
	
4. Generate Diffie-Hellman parameters (dh2048.pem).
	
		$ ./build-dh

5. Generate a random key for sharing (ta.key)
		
	
	$ openvpn --genkey --secret keys/ta.key
	
6. Copy the files to the OpenVPN folder (in Ubuntu):
		
	
		$ sudo cp keys/{server.crt,server.key,ca.crt,dh2048.pem,ta.key} /etc/openvpn

--

- Configurate OpenVPN by extracting an example file:

		$ gzip -d -c /usr/share/doc/openvpn/examples/sample-config-files/server.conf.gz | sudo tee /etc/openvpn/server.conf > /dev/null

Check that the /etc/openvpn/server.conf file contains the following

		ca ca.crt
		cert server.crt
		key server.key  # This file should be kept secret
		dh dh2048.pem

- Setup firewall (Ubuntu FireWall). 
	Enable it manually:
		
		sudo vim /etc/ufw/ufw.conf
	
	Change the following 
		
		ENABLED=no
	to
		ENABLED=yes
		
	The following command allows incoming traffic from port 1194/udp (default port and protocol):
		
		$ sudo ufw allow openvpn
	
	Edit the server configuration file  (/etc/openvpn/server.conf): 
	uncomment the following line:
	
		push "redirect-gateway def1 bypass-dhcp"
	
	Set up iptable rule (eth0 is adjustable here) to NAT the VPN client.
	
		$ sudo iptables -t nat -A POSTROUTING -s 10.8.0.0/24 -o eth0 -j MASQUERADE
	
	Edit rules for ufw (Ubuntu FireWall); insert the following lines at the 
	beginning of the file "/etc/ufw/before.rules" (use sudo vim command) :
	
		*nat
		:POSTROUTING ACCEPT [0:0] 
		-A POSTROUTING -s 10.8.0.0/8 -o eth0 -j MASQUERADE
		COMMIT		

	uncomment the line 28 of the file /etc/sysctl.conf, so it becomes:
		
		# Uncomment the next line to enable packet forwarding for IPv4
		net.ipv4.ip_forward=1
	
	reload the configuration:
	
		$ sudo sysctl -p /etc/sysctl.conf
	
	Allow packet through the ufw; change the following section to ACCEPT 
	in /etc/default/ufw:
	
		# Set the default forward policy to ACCEPT, DROP or REJECT.  Please note that
		# if you change this you will most likely want to adjust your rules
		DEFAULT_FORWARD_POLICY="ACCEPT"
	
	Reload firewall (it should say "firewall reloaded"):
		
	
		$ sudo ufw reload
	
- Start (stop) the service
		
		$ sudo systemctl start openvpn@server
	
	Use the following command to check the status:
		
	
		$ sudo systemctl is-active openvpn@server
	
- Prepare documents for clients (still in the certificate folder):
		
		$ source vars && ./build-key client
	
	Extract the example document:
		
		$ mkdir clients && cp /usr/share/doc/openvpn/examples/sample-config-files/client.conf clients/client.ovpn
	
	The rest of steps are done in the clients/client.ovpn file:
	
	Edit line 42:
		
		remote my-server-1 1194
	
	replace my-server-1 with ip address (wlan0 ip works):
		
		remote ip 1194
	
	uncomment lines 61,62:
		
		# Downgrade privileges after initialization (non-Windows only)
		;user nobody
		;group nogroup

	comment lines 88-90 and 108:
	
		#ca ca.crt
		#cert client.crt
		#key client.key
		#tls-auth ta.key 1

	Lookup certificate/key folder, copy contents in 
	ca.crt, client.crt, client.key, ta.key into clients/client.ovpn:
		
		<ca>
		# Here goes the content of the ca.crt file
		</ca>
		
		<cert>
		# Here goes the content of the client.crt file
		</cert>
		
		<key>
		# Here goes the content of the client.key file
		</key>
		
		key-direction 1
		<tls-auth>
		# The content of the ta.key file
		</tls-auth>
	
- Last step! Let the phone use OpenVPN to import this .ovpn file to build connection!

Trouble shooting:

- Search for NDS: adjust ip address in the .ovpn file.
- waiting for server, activiate server via
		
		$ sudo systemctl start openvpn@server
	
### Set up SSH keypairs (auto log in)
0. Generate a SSH Key:

see gitHub:

https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/

*One key for each server, and the name of id_rsa can be changed; just remember to add it after rename it.*

1. Intro:

id_rsa: private key that NEVER share.
id_rsa.pub: public key that stores in the remote server.

2. Paste public key to remote server.

Paste the id_rsa.pub to the following location of the remote server:

	~/.ssh/

the file needs to be named as <u>authorized_keys</u>.

change permission:
	
	chmod 600 authorized_keys

##### For <u>mac</u>, edit config file in the local ~/.ssh/

	Host *
	 AddKeysToAgent yes
	 UseKeychain yes
	 IdentityFile ~/.ssh/id_rsa

 *id_rsa is the name of the key to be verified.*

##### Shortcut for the log in:

For example, I want to use $ssh k$ to log in:

	Host k
	    User account
	    IdentityFile .ssh/id_rsa
	    HostName server 

---
## Got a Problem?
* [Mac](#mac-issue)


### Mac Issue
Incorrect directory for an app? Try:
> `export PATH="/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin"`

Error: unrecognized command-line option '-stdlib=libc++'
> I think I mess up gcc..

### C++ compiler
`error: ld returned 1 exit status`
> Function is not defined, try a dummy definition.
