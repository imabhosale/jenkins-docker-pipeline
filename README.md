
# Jenkins Docker PipeLine
## Create Jenkins Pipeline to Run Docker Image



## Step-by-Step Process:
#### Prerequisites
AWS EC2 Instance \
Java Installed

### Create a New Pipeline in Jenkins locally
1 ) Open Jenkins dashboard.\
2 )  Select New Item, name it, and choose Pipeline.\
3 ) Click OK\
4 ) Define the Jenkins Pipeline use sample hello world script\
5 ) Build pipeline and see console output

### Create Jenkins Pipeline to Run Docker Image from a GitHub Repo
1 ) Create a GitHub Repository:\
2 ) Clone the repo locally\
```bash
    git clone https://github.com/imabhosale/jenkins-docker-pipeline.git
```
3 ) Create a Jenkinsfile in repository and add the following pipeline code: 
```bash
pipeline {
    agent {
        docker {
            image 'node:20.16.0-alpine3.20'
        }
    }
    stages {
        stage('Test') {
            steps {
                sh 'node --version'
            }
        }
    }
}
```
4 ) Push Code to GitHub
```bash 
git add .
git commit -m "Initial commit for Jenkins Docker pipeline"
git push origin main
```

5 ) Create a New Pipeline in Jenkins: name it , click OK\

6)Configure GitHub SCM in Jenkins:\
Scroll to the Pipeline section.\
Select Pipeline script from SCM.\
Choose Git as the SCM\
Paste your GitHub repository URL (https://github.com/imabhosale/jenkins-docker-pipeline)\
Enter your GitHub credentials if needed.\
Set the branch to main.

6 )Build the Pipeline: Click Save and then Build Now.

 ## Jenkins pipeline on EC2 (VM)

1)  Install Jenkins\
SSH into your EC2 instance and run the following commands:
```bash 
# Update system packages
sudo yum update -y

# Install Java (required for Jenkins)
sudo amazon-linux-extras install java-openjdk11 -y

# Add Jenkins repository
sudo wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo

# Import Jenkins key
sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io-2023.key

# Install Jenkins
sudo yum install jenkins -y

# Start and enable Jenkins
sudo systemctl start jenkins
sudo systemctl enable jenkins
```
2) Configure Jenkins:\
Open your browser and go to http://<EC2-Instance-Public-IP>:8080
```bash 
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```
3)  Install Docker on EC2
```bash 
# Install Docker
sudo yum install docker -y

# Start and enable Docker service
sudo systemctl start docker
sudo systemctl enable docker

# Add Jenkins user to the Docker group so Jenkins can run Docker commands
sudo usermod -aG docker jenkins

# Restart Jenkins to apply group changes
sudo systemctl restart jenkins
```
Verify Docker Installation:

do above steps from github or check manually 

 ## History Of command used in practical
 ```bash 
   1  chmod 400 demo.pem
    2  exit
    3  sudo yum install -y
    4  sudo yum install git -y
    5  sudo yum update -y
    6  git config --global user.name "Abhishek Bhosale"
    7  git config --global user.email "abhishekbhosale676@gmail.com"
    8  git config ls
    9  git config --list
   10  sudo dnf install java-17-amazon-corretto -y
   11  sudo wget -O /etc/yum.repos.d/jenkins.repo
   12  sudo yum update -y
   13  sudo wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo
   14  sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io-2023.key
   15  sudo yum install jenkins -y
   16  jenkins --version
   17  sudo systemctl start jenkins
   18  sudo systemctl enable jenkins
   19  sudo cat /var/lib/jenkins/secrets/initialAdminPassword
   20  clear
   21  sudo yum install docker -y
   22  sudo systemctl start docker
   23  sudo systemctl enable docker
   24  sudo usermod -aG docker jenkins
   25  sudo systemctl restart jenkins
   26  history
```

