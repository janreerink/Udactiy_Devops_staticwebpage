# static
for udacity devops nanodegree

## Prepare AWS 
- Create IAM user, log in with new user. Create key-pair and launch EC2 instance.
  ![img1](data/screenshot-01.png)
  
- Create security group for new instance:  
  - add TCP inbound rule, port 8080, source 0.0.0.0/0
  - add SSH rule, port 22, source 'my ip'

  ![img2](data/screenshot-02.png)

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
  ![img3](data/screenshot-03.png)
## Setup jenkins
- Navigate to port 8080 on EC2 instance
- Use `sudo cat /var/lib/jenkins/secrets/initialAdminPassword` to retrieve install pwd, create new admin
- Install suggested plugins, then manually add Blue Ocean Aggregator and pipeline-aws
  ![img4](data/screenshot-04.png)

## Set up github repo for static website
- With index.html and jenkinsfile
- Connect git to jenkins (preferably using github access token) to build pipeline. Change pipeline to check repo for changes every 2 minutes.
  ![img5](data/screenshot-05.png)
## Setup jenkins credentials in AWS
- In Jenkins credentials menu select global, aws from dropdown and use key generated in AWS IAM
  
## Setup S3 bucket
- Create new S3 bucket without public access restrictions, note name and region
- In properties configure for static website hosting with index.html
- Enter following bucket policy:
```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "PublicReadGetObject",
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::bucketforudacitydevopsnanodegreejenkinsproject/*"
        }
    ]
}
```
  ![img6](data/screenshot-06.png)

## modify jenkinesfile
- add withaws and s3upload to change the pipeline and test it
- install tidy for linting  
`sudo apt-get install -y tid`
- change jenkinsfile to add html linting stage, this finds the error in the original html and breaks the build:  
![img7](data/screenshot-07.png)
- finally, fix error in html; linting stafe should complete now  
![img8](data/screenshot-08.png)


