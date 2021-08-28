# jenkins-quickstart
Jenkins Quickstart


## Installation

Go to [jenkins.io](jenkins.io)

Click download and select your OS

### Ubuntu setup

This is the Debian package repository of Jenkins to automate installation and upgrade. To use this repository, first add the key to your system:
```sh
 wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo apt-key add -
```

Then add a Jenkins apt repository entry:
```sh
sudo sh -c 'echo deb https://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
```

Update your local package index:

```sh
sudo apt-get update
```

Jenkins require java installed

#### Install Java

Execute the following command to install the default Java Runtime Environment (JRE), which will install the JRE from OpenJDK
```sh
sudo apt install default-jre
```

You may need the Java Development Kit (JDK) in addition to the JRE in order to compile and run some specific Java-based software.
```sh
sudo apt install default-jdk
```

#### Complete jenkins installation
```sh
sudo apt-get install jenkins
```

Check the service

```sh
sudo service jenkins restart
sudo service jenkins status
```

After the installation, jenkins will be running on your machine on:

[http://localhost:8080/](http://localhost:8080/)


If it cant be served on this port:

Install Nginx and allow port 8080 on your firewall

```sh
sudo apt install nginx -y

sudo service nginx start
sudo service nginx status
```

```sh
sudo ufw allow 8080
```

You show now have it running on:
[http://localhost:8080/](http://localhost:8080/)


### Getting started

From the prompt to show the initial secure password. Head on to your terminal and type:

```sh
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

It will generate a password to login.

Select the suggested plugin installation.

After that, create your admin user and you should land on the dashboard now. 


### Running Build Commands Locally
Check if the jenkins user has access to bash
```sh
getent passwd jenkins

#output
jenkins:x:129:138:Jenkins,,,:/var/lib/jenkins:/bin/false

#give it bash access
sudo usermod -s /bin/bash jenkins

getent passwd jenkins
#output
jenkins:x:129:138:Jenkins,,,:/var/lib/jenkins:/bin/bash


##get jenkins passwd
sudo passwd jenkins

sudo su - jenkins
#we should now be in the jenkins user shell


##Generate ssh keys
ssh-keygen
#follow the prompt
```

Try to see if you can login via ssh

```sh
ssh-copy-id jenkins@localhost

#output
/usr/bin/ssh-copy-id: INFO: Source of key(s) to be installed: "/var/lib/jenkins/.ssh/id_rsa.pub"
The authenticity of host 'localhost (127.0.0.1)' can't be established.
ECDSA key fingerprint is SHA256:HGGHGHDHGafdsfdgdsFSHFG+HGHSFHSHGF
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
/usr/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed
/usr/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted now it is to install the new keys
jenkins@localhost's password: 

Number of key(s) added: 1

Now try logging into the machine, with:   "ssh 'jenkins@localhost'"
and check to make sure that only the key(s) you wanted were added
```

Let's try to login:

```sh
ssh jenkins@localhost
```

```sh
jenkins@ktechhub:~$ ssh jenkins@localhost
Welcome to Ubuntu 21.04 (GNU/Linux 5.11.0-25-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

88 updates can be applied immediately.
To see these additional updates run: apt list --upgradable

*** System restart required ***
jenkins@ktechhub:~$
```

We need the ssh to allow Jenkins run builds locally. Jenkins will conduct these builds over ssh

Finally: Let's add jenkins to the sudo groups... 

I am going to add jenkins with NOPASSWD. You should tailor this to your application needs but since this is just a quickstart, I will just allow all commands for the jenkins user. 

```sh
sudo visudo

#append the jenkins user

# User privilege specification
root    ALL=(ALL:ALL) ALL
jenkins ALL=(ALL) NOPASSWD:ALL
```




