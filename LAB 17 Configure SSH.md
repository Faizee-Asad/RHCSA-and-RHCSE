# Before configure let's understand Port Number and Sockets

## Port Number and Sockets
* Every server has unique IP address.
* We caa run multiple network application on a single server.
* All applications on a single server use single IP address.
* So, to bring further uniqueness in communication, every application uses another address called **port number**.
* Application Port Number range from 1 to 65535.
* Well-Known ports: 1 - 1023. e.g SSH (22), HTTP (80), HTTPS(443).
* Port above 1023 are used for session management and custom port assigning.
* So, application use their unique port numbers on Server IP address to talk to clients.
* Almost all network applications are service based.
```
Network Application --> Services -- > Process (PID) --> Port Number (Listen) = Socket
```
* Also, every network applications has a config file from where it takes all the instrutions. (/etc)
* Whenever we modify the config file of an application, it is must to restart its service.
* To start their process, we need to start their service
```
A process of a network application listening client requests on its port number is called a socket.
In Linux, applications like netstat and ss are used to list all open sockets of a server.
Commands:
# netstat -n
# ss -tnlp
```
* Netwrok applications are either TCP based (User auth is must) or UDP based (User auth is optionally).

## Remote services

* Remote server helps admins and developers to access server remotely over an IP netwrok.
* Since Linux server run on command line, admins and developer take CLI remote access of servers for administration and application development purpose.
* There are plenty of opensorce tools on Linux for CLI remote access like **telnet, RSH, rlogin and SSH**.
* Telnet was the 1st ever remote service that existed. But due to its unsecured behavior, it is not preferred nowadays. (Clear text format)
* SSH is the most preferred remote service , as it is secured. (encryptd data)

```

Datacenter         <----------   Remote access                   office Premise
  Server --> ab,cd,ef,gh         IP Network         <------          Admin PC

```
## Secure Shell (SSH)
* SSH is a remote sevice
* It is used for remote CLI access of linux servers.
* It works on server-client scenario.
* SSH server is installed on linux servers.
* SSH client is installed on admin computer.
* It is a TCP based service. Hence, it requires user authenrication to login.
* The server application uses TCP port 22 to connect with clients.
* SSH is the most secured service for remote access as it provides end-to-end data encryption throughout the session.
* On Linux, openssh tool is used  on both server and client.
* On Windows, client tools like putty (free) and secureCRT (paid) are used as SSH client.
* By default, SSH allows root login

## SSH authentication methods:
* There are 2 authentication methods for SSH login.
  1. Password authentication.
  2. Key-Pair authentication.
* Password authentication is the default method.
* Password authentication is not a safer way to use SSH as password (through in encrypted form) travels over the network or internet. Hence, there is still a chance of the password getting trapped.
* The more secure way is to use SSH keypair authentication
* In this method, a keypair is generated on client machine.
* The keypair will have a private key and a public key.
* Public key should be stored on server and private key should be stored on client
* When client with a private key will send request to server, the server will authenticate client with the keypair and will not require password.
* Key does not travel on network unlike the password. Hence, this method is more secured.
```
Ketpair
  |----- private key (id_rsa_file)
  |----- public key (id_rsa.pub file)
```
# Task 1: Configure SSH on server

* Step 1: Check whether openssh is installed
```
# dnf list openssh
```
* Step 2: Check whether openssh is running (if not enable it.):
```
# systemctl enable --now sshd
# systemctl status sshd
# ps -el|grep sshd
# ss -tnlp			(check the sockets for port 22 and their PID numbers)
```
# Task 2: On client side (Linux)

* Step 1: Check whether openssh is installed
```
# dnf list openssh
```
* Step 2: Connect to server remotely.
```
# ssh root@10.0.0.50	   #10.0.0.50 can be replaced with destination server address and root can be replaced with any remote user
# yes
## provide password of the user
# exit
```
* Step 3 : To run a command on remote server rather than taking a persistent SSH session
```
# ssh root@10.0.0.50  'touch /usr/local/123.txt' 		to run a command on remote server rather than taking a persistent SSH session
# ssh root@10.0.0.50  'ls /usr/local'
```

* Step 4: To copy and paste client to server and server to client
```
touch aaa.txt
	scp aaa.txt   root@10.0.0.111:/root				to copy a file from client to server
	scp root@10.0.0.111:/root/aaa.txt   /usr			to copy a file from server to client
```
# Task 3: Keypair Authentication

* Step 1 : On Linux client: (10.0.0.100) generate a keypair
```
# ssh-keygen											to generate a keypair on client
enter > enter > enter
```
* Step 2: Locate the keys
```
# ls .ssh
# cat .ssh/id_rsa										check private key
# cat .ssh/id_rsa.pub									check public key
```
* Step 3: transfer public key on server
```
# ssh-copy-id root@10.0.0.111							to transfer public key on server
# ssh-copy-id root@10.0.0.112							to transfer public key on server	
# ssh-copy-id root@10.0.0.50							to transfer public key on server
# ssh root@10.0.0.111									keypair based login
```
* Step 4: Enforce keypair authentication only
```
On server side (10.0.0.111, 10.0.0.112, 10.0.0.50): to enforce keypair authentication only
	vi /etc/ssh/sshd_config
			uncomment and change PASSWORD_AUTHENTICATION=yes to PASSWORD_AUTHENTICATION=no
	systemctl restart sshd
```

_______________________________________________________________________________________________________________________
```
SSH:
On server: (10.0.0.111, 10.0.0.112, 10.0.0.50)
	dnf list openssh
	systemctl enable --now sshd
	systemctl status sshd
	ps -el|grep sshd
	ss -tnlp			(check the sockets for port 22 and their PID numbers)

On client side (Linux): (10.0.0.100)
	dnf list openssh 
	ssh root@10.0.0.50	   #10.0.0.50 can be replaced with destination server address and root can be replaced with any remote user
	yes
	provide password of the user
	exit

	ssh root@10.0.0.50  'touch /usr/local/123.txt' 		to run a command on remote server rather than taking a persistent SSH session
	ssh root@10.0.0.50  'ls /usr/local'
	touch aaa.txt
	scp aaa.txt   root@10.0.0.111:/root				to copy a file from client to server
	scp root@10.0.0.111:/root/aaa.txt   /usr			to copy a file from server to client



Keypair Authentication:
On Linux client: (10.0.0.100)
	ssh-keygen											to generate a keypair on client 
		enter > enter > enter
	ls .ssh
	cat .ssh/id_rsa										check private key
	cat .ssh/id_rsa.pub									check public key
	ssh-copy-id root@10.0.0.111							to transfer public key on server
	ssh-copy-id root@10.0.0.112							to transfer public key on server	
	ssh-copy-id root@10.0.0.50							to transfer public key on server
	ssh root@10.0.0.111									keypair based login

On server side (10.0.0.111, 10.0.0.112, 10.0.0.50): to enforce keypair authentication only
	vi /etc/ssh/sshd_config
			uncomment and change PASSWORD_AUTHENTICATION=yes to PASSWORD_AUTHENTICATION=no
	systemctl restart sshd
```
