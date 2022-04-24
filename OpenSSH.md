# Instructions to set up an SSH server and client with OpenSSH

Info on OpenSSH. Includes how to set up an ssh server, ssh key-based authentication and more.

## On the Client side

### Install the required packages

Look for SSH binaries
~~~
which ssh
~~~
Check if the OpenSSH client is installed 
~~~
apt search openssh-client
~~~
If it's installed you will see something like this:

![OpenSSH installed](images/OpenSSH_installed.jpg)

If not, install some updates first
~~~
 sudo apt update && sudo apt upgrade 
~~~
And then install the OpenSSH client
~~~
sudo apt install openssh-client
~~~
### Connect to an SSH server
Since we have the client already installed, run:
~~~
ssh username@ipadress 
~~~
In my case I will long in to an AWS EC2 instance using ssh key authentication (more on this later) so it looks like this:

![Login into EC2 instance](images/Logging_ssh_server.jpg)

As long as the server is running and accepting incoming traffic on the port **22** you should at least get a password prompt. Whenever we connect for the first time it will ask us if we are sure we want to connect.

If this is the first time we connect to an ssh server, in the client, we will now have a .ssh folder that includes a **known_hosts** file. 

![Known Hosts](images/Known_hosts.jpg)

This file contains the fingerprint of all the SSH servers we have connected to. If we connect again to the same server, 
this time it won't ask if we are sure if we want to connect since the info is already in the **known_hosts** file. 

This is important because it prevents a man-in-the-middle attack. Let's say someone creates a malicious server and they were able to set our same ip address, if that's the case, when we try to connect, Ubuntu will see that out fingerprint has changed and when that happens it will raise a warning.

### Locating the auth.log file

In the client, when log into the server

![Login again](images/Auth_log_1.jpg)

Locate the log directory
~~~
cd /var/log/
~~~

When we run
~~~
tail -f auth.log
~~~
we can track the changes for the auth.log for every login attempt

![Login again](images/Auth_log_2.jpg)

This file is very important since it allows to see what is going on whenever we attempt to connect to the server.

### Configuring the OpenSSH Client

Let's create a config file for the SSH client. Move into the .ssh folder
~~~
cd .ssh
~~~
Create the config file
~~~
touch config
~~~
And change the file this way
![SSH config](images/ssh_config.jpg)
Now instead of doing
~~~
ssh username@ipadress
~~~
or 
~~~
ssh -i "public_key" username@ipadress
~~~
We can just say 
~~~
ssh sshserver
~~~
Since I'm using a Public Key on my side it looks like this:
![Login with public key](images/ssh_config_2.jpg)

**Note** that the Host variable at the end can have whatever name you want.
Let's change the said variable this way:
![Changing the host variable](images/ssh_config_3.jpg)

Now when I run:
~~~
ssh -i "public_key" newsshserver
~~~
We can see we are able to log in
![Login with new Host variable](images/ssh_config_4.jpg)