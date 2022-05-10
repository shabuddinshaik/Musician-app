# musician-app
NodeJS / React sample app for AWS CI/CD pipeline tutorial

Configure Jenkins Slaves on AWS EC2
Jenkins is a self-contained Java-based program, ready to run out-of-the-box, with packages for Windows, Mac OS X and other Unix-like operating systems. As an extensible automation server, Jenkins can be used as a simple CI server or turned into the continuous delivery hub for any project.

Follow this article in Youtube
Jenkins Master and Slave Configuration

Prerequisites
Jenkins Master Running Get help here
EC2 RHEL 7.x Instance - for Slave Node Get help here
With Internet Access
Security Group with Port 8080 open for internet
Java v1.8.x
Install Java
We will be using open java for our demo, Get latest version from http://openjdk.java.net/install/. Also configure the default JAVA_HOME path

apt install java-1.8*
#yum -y install java-1.8.0-openjdk
Setup Jenkins Slave
# Create user and add the user to wheel group
useradd jenkins-slave-01
# Create SSH Keys
sudo su - jenkins-slave-01
ssh-keygen -t rsa -N "" -f /home/jenkins-slave-01/.ssh/id_rsa
# The private and public keys will be created at these locations `/home/jenkins-slave-01/.ssh/id_rsa` and `/home/jenkins-slave-01/.ssh/id_rsa.pub`
cd .ssh
cat id_rsa.pub > authorized_keys
chmod 700 authorized_keys
Configuration on Master
Copy the slave node's public key[id_rsa.pub] to Master Node's known_hosts file

mkdir -p /var/lib/jenkins/.ssh
cd /var/lib/jenkins/.ssh
ssh-keyscan -H SLAVE-NODE-IP-OR-HOSTNAME >>/var/lib/jenkins/.ssh/known_hosts
# ssh-keyscan -H 172.31.38.42 >>/var/lib/jenkins/.ssh/known_hosts
chown jenkins:jenkins known_hosts
chmod 700 known_hosts
Configure the Slave using Manage Jenkins
Configure the node as shown here Manage Jenkins > Manage Nodes > New Node Jenkins Master and Slave Configuration

