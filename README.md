# Complete DevOps CICD Project
Using Github, Jenkins, Maven, Docker
![Developer](https://github.com/rutikdevops/DevOps-Project-1/assets/109506158/ffad3632-0976-413c-99e6-7b36f01a16bd)

# Detailed Blog Link:

# Steps pf this project:

Create 4 ec2 instance name as:- (AWS Linux-2, t2 micro)
1. Jenkins-Server
2. Ansible-Server
3. Web-Server
4. Developer
<img width="959" alt="image" src="https://github.com/rutikdevops/DevOps-Project-1/assets/109506158/ad8f8f16-d059-4b7d-9bb2-b64c39bb2d8f">

<br></br>
# 1. Connect Jenkins server with putty:-
```bash
  ec2-user
sudo su
yum update -y
hostnamectl set-hostname jenkins
bash
```


Java installation on Jenkins server:-
```bash
yum install java* -y
java --version
alternatives --config java               ## Using this command you can choose any version of Java
```

Jenkins installation on Jenkins server:-
```bash
wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo
rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io-2023.key
yum install jenkins -y
systemctl enable jenkins.service
systemctl start jenkins.service
systemctl status jenkins.service
```bash

Copy public ip of jenkins server with port no.8080
15.207.51.80:8080










