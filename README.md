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
# 1. Connect Jenkins server with putty :-
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
```

Copy public ip of jenkins server and paste it in new tab with port no.8080
<img width="382" alt="image" src="https://github.com/rutikdevops/DevOps-Project-1/assets/109506158/1abe6c22-642f-44b6-be2f-4514f1c35e4a">

- copy this path and paste in terminal with "cat" command
```bash
cat /var/lib/jenkins/secrets/initialAdminPassword
```
- Now copy & paste this passwd in jenkins. so, jenkins is ready.
<br></br>



# 2. Connect Ansible server with putty :-
```bash
ec2-user
sudo su
yum update -y
hostnamectl set-hostname Ansible
bash
```
Ansible installation on Ansible server:-
```bash
yum install ansible -y
amazon-linux-extras install ansible2 -y
ansible --version
```

Now go to inventory file and add entry of web server
```bash
vim /etc/ansible/hosts
```
In that inventory file you can simply add 
```bash
[web]
(paste here web-servers private ip)
```



# 3. Connect web server with putty :-
```bash
ec2-user
sudo su
yum update -y
hostnamectl set-hostname web-server
bash
```
httpd Apache installation on web-server:-
```bash
yum install httpd -y
systemctl enable httpd
systemctl start httpd
```


# 3. Passwordless connection between Ansible & Web server :-
- Go to ansible server and type command
ssh-keygen (and press enter 2 to 3 times)
ssh-copy-id -i root@(paste web-server private ip here)

- Go to web-server and type command
passwd root (Now enter passwd 2 times)
vim /etc/ssh/sshd_config
** #PermitRootLogin yes          (remove #)
** PasswordAuthentication no     (replace no to yes)
systemctl restart sshd



```bash
```









