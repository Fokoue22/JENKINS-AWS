# JENKINS-AWS
This repository will contain all jenkins project on AWS 


## Deploy Jenkin in ubuntu ec2 instance 
We first need to create and ec2 instance on AWS. The EC2 instance must be launche in a `PUBLIC subnet` and should be attache to a SG with inbound role `TCP on port 8080 to your IP address` and `SSH on port 22 to 0.0.0.0/0`. Then we install jenkins by using the following steps below or by going to the official documentation Read [this page](https://www.jenkins.io/doc/book/installing/linux/#debianubuntu) for more information about the syntax to use.

## `NB` In case we are working with Linux-ec2-instance we change the package manager of ubuntu `apt` to linux `yum`.

## Environment variable
### `In steps 1` `INSTALL JAVA SDK` 
1. We first need to update the OS
```
sudo apt update

```
2. Then we install java package 
```
sudo apt install java-17-amazon-corretto-devel -y

```
3. Verified of the java package was succesfully install 
```
java -version

```
### `In steps 2`  `ADD JENKINS TO DEBIAN REPO`
1. We do this by using the Long term support release 
```
sudo wget -O /usr/share/keyrings/jenkins-keyring.asc \
  https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key

```
2. 
```
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null

```
### `In steps 2`  `ADD JENKINS TO Red Hat package.`
1. Install Jenkins on an Amazon Linux 2 AMI EC2 instance using the [official guide](https://www.jenkins.io/doc/book/installing/linux/#red-hat-centos).
```
sudo wget -O /etc/yum.repos.d/jenkins.repo \https://pkg.jenkins.io/redhat-stable/jenkins.repo
```
```
sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io-2023.key
```
```
sudo yum install jenkins
```
### `In steps 3` `INSTALL JENKINS`
1. We first update the libriaries 
```
sudo apt-get update

```
2. install jenkins  
```
sudo apt-get install jenkins -y

```
3. This command will check if jenkins has been install and working `DON'T FORGET TO COPY AND SAVE THE ADMIN PASSWORD` It may also be found  `/var/lib/jenkins/secrets/initialAdminPassword`
```
sudo systemctl status jenkins

```
4. start jenkins `enable` allow you to state the service automatically when the system bot up or when you bot up the system 
```
sudo systemctl enable jenkins

```

### `In steps 3` `ENABLE PORT 8080 ON HOST FIREWALL`
1. We first update the libriaries. `ufw` this is a virtual firewall on ubuntu instance 
```
sudo ufw enable -y

```
2. Then we allow port `8080`. This will allowed all incomming requese coming from this port. We do this because by default http run on port 80 while jenkins on port 8080. So we must always indicate the port of jenkins if not it will not work   
```
sudo ufw allow 8080

```
3. Then we may also need to open SSH   
```
sudo ufw allow openSSH

```

## Author
FOKOUE THOMAS 