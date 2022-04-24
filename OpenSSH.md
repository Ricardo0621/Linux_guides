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

If this is the first time we connect to an ssh server, in the client, we will now have a .ssh folder that includes a known_hosts file. 

This file contains the fingerprint of all the SSH servers we have connected to. If we connect again to the same server, 
this time it won't ask if we are sure if we want to connect since the info is already in the **known_hosts** file. 

![FIle](images/Known_hosts.jpg)
