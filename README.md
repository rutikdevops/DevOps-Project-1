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

set root passwd
```bash
passwd root     
```
Now, enter passwd 2 times
```bash
vim /etc/ssh/sshd_config
```
Do this changes in vi editor:-
** #PermitRootLogin yes          (remove #)
** PasswordAuthentication no     (replace no to yes)
Now run this command:-
```bash
systemctl restart sshd
```


git installation on Jenkins server:-
```bash
yum install git -y
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


# 4. Passwordless connection between Ansible & Web server :-
- Go to ansible server and type command
```bash
ssh-keygen (and press enter 2 to 3 times)
```
```bash
ssh-copy-id -i root@(paste web-server private ip here)
```

- Go to web-server and type command
```bash
passwd root (Now enter passwd 2 times)
```
```bash
vim /etc/ssh/sshd_config
```
Do this changes in vi editor:-
** #PermitRootLogin yes          (remove #)
** PasswordAuthentication no     (replace no to yes)
Now run this command:-
```bash
systemctl restart sshd
```

- Go to ansible server and type command
```bash
ssh-copy-id -i root@(paste web-server private ip here)
```
enter passwd
```bash
root@(paste web-server private ip here)
```
```bash
exit    //for go to web-server to ansible
```
Now, your Passwordless connection between Ansible & Web server is successfull



# 5. Passwordless connection between Jenkins to Ansible server :-
Follow same steps from point no. 4 for jenkins to ansible connection


# 6. Create a Playbook in ansible server:-
create a directory in ansible
```bash
mkdir /sourcecode
```
Go to sourcecode directory
```bash
cd /sourcecode
```
Now, create a playbook name as,
```bash
playbook.yml
```
In playbook.yml file type,
```bash
- hosts: all
  tasks:
    - copy:
         src: /opt/index.html
         dest: /var/www/html
```



# 7. Create a Github repo:-
Github>> Create repo>> DevOps-Project-1(repo name)
Create new file>>index.html(file name)
In this file write,
```bash
My Name is Rutik
```


# 8. Integrate Github with Jenkins:-
Github>> Settings>> Webhooks
Payload URL:- (paste jenkins URL here)
content type:- Application/json
Secret:- Go to jenkins>>configure>>API Token>>add token>>copy token>>apply>>save ===> Paste this token
Add Webhook>>click on page refresh



# 9. Install plugin in jenkins:-
Manage_jenkins>> Plugins>> available plugin>> publish over SSH>> restart jenkins

# 10. Create project in Jenkins:-
New_Item>> Project-1(Item_name)>> Freestyle_Project
Source code mangmt>> copy code URL from github

Manage_jenkins>> Configure_system
![image](https://github.com/rutikdevops/DevOps-Project-1/assets/109506158/1ef373ec-d1de-4bf8-be4e-8cd67cb1e0ec)

Project-1>>configure>>build>>Send files or execute commands over SSH
![image](https://github.com/rutikdevops/DevOps-Project-1/assets/109506158/f5cef71f-9dab-46dc-b0ca-5c3c1a98f5b1)
Exec command:- rsync -avh /var/lib/jenkins/workspace/project-1/*.html root@(paste ansible private ip here):/opt/index.html




Manage_jenkins>> Configure_system
![image](https://github.com/rutikdevops/DevOps-Project-1/assets/109506158/d97a33eb-4da2-4722-b194-67bc2bcb121c)

Project-1>>configure>>Post-build Actions>>Send build artifacts over SSH
![image](https://github.com/rutikdevops/DevOps-Project-1/assets/109506158/1011e86b-a70a-42bd-9418-dbd66c2364cd)














```bash
```
