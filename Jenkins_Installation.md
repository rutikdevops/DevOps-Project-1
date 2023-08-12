```bash
ec2-user
sudo su
yum update -y
hostnamectl set-hostname jenkins
bash
```

```bash
//Java installation
yum install java* -y
java --version
alternatives --config java               ## Using this command you can choose any version of Java
```

```bash
//jenkins installation
wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo
rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io-2023.key
yum install jenkins -y
systemctl enable jenkins.service
systemctl start jenkins.service
systemctl status jenkins.service
```
