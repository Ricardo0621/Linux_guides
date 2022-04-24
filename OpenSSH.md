# Instructions to set up an SSH with OpenSSH

Info on OpenSSH. Includes how to set up an ssh server, ssh key-based authentication and more.

## On the Client side

### Install the required packages

Look for SSH binaries
~~~
which ssh
~~~

Check if OpenSSH client is installed 

~~~
apt search openssh-client
~~~
If it's installed you will see something like this:

![OpenSSH installed](images/OpenSSH_installed.jpg)

If not, install the OpenSSH client
~~~

~~~


~~~
 sudo apt update && sudo apt upgrade 
~~~
