# static
for udacity devops nanodegree

## Prepare AWS 
- Create IAM user, log in with new user. Create key-pair and launch EC2 instance.
- Create security group for new instance:  
  - add TCP inbound rule, port 8080, source 0.0.0.0/0
  - add SSH rule, port 22, source 'my ip'

## Install Jenkins on EC2
- Update OS, install JDK, get the repo for latest Jenkins version, install and verify service is running.
- `sudo apt update`
- `sudo apt upgrade`
- `sudo apt install default-jdk`
- `wget -q -O - https://pkg.jenkins.io/debian/jenkins.io.key | sudo apt-key add -`
- `sudo sh -c 'echo deb http://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'`
- `sudo apt update`
- `sudo apt install jenkins`
- `sudo systemctl status jenkins`

## Setup jenkins
- Navigate to port 8080 on EC2 instance
- Use `sudo cat /var/lib/jenkins/secrets/initialAdminPassword` to retrieve install pwd, create new admin
- Install suggested plugins, then manually add Blue Ocean Aggregator and pipeline-aws

## Set up github repo for static website
- With index.html and jenkinsfile
