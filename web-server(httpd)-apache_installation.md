ec2-user
sudo su
yum update -y
hostnamectl set-hostname web-server
bash

//apache installation
yum install httpd -y
systemctl enable httpd
systemctl start httpd
