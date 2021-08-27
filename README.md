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

