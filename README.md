# zomato-clone-devops-deployment
Launch an Instance (Ubuntu, 24.04, t2.large, 30 GB)
Launch an Instance (Ubuntu, 24.04, t2.large, 30 GB)

Connect to the instance

Update the packages
$ switch to root user ---> sudo su
$ sudo apt update -y

Install AWS CLI
sudo apt install unzip -y
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install

5. Install Jenkins on Ubuntu
(Reference URL for commands: https://www.jenkins.io/doc/book/installing/linux/#debianubuntu)
#!/bin/bash
sudo apt update -y
wget -O - https://packages.adoptium.net/artifactory/api/gpg/key/public | sudo tee /etc/apt/keyrings/adoptium.asc
echo "deb [signed-by=/etc/apt/keyrings/adoptium.asc] https://packages.adoptium.net/artifactory/deb $(awk -F= '/^VERSION_CODENAME/{print$2}' /etc/os-release) main" | sudo tee /etc/apt/sources.list.d/adoptium.list
sudo apt update -y
sudo apt install temurin-17-jdk -y
/usr/bin/java --version
curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee /usr/share/keyrings/jenkins-keyring.asc > /dev/null
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] https://pkg.jenkins.io/debian-stable binary/ | sudo tee /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update -y
sudo apt-get install jenkins -y
sudo systemctl start jenkins
sudo systemctl status jenkins

--give permissions for jenkins.sh file 'chmod +x jenkins.sh'
-- to excute shell file './jenkins.sh'
Verifiy Jenkins installation: jenkins --version

5.1. Open Port No. 8080 for VM and access Jenkins
5.2. Setup Jenkins by following the necessary steps

6. Install Docker on Ubuntu
(Reference URL for commands: https://docs.docker.com/engine/install/ubuntu/)

# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc
# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin -y
sudo usermod -aG docker ubuntu
sudo chmod 777 /var/run/docker.sock
newgrp docker
sudo systemctl status docker

Verifiy Docker installation: docker --version

7. Install Trivy on Ubuntu
(Reference URL for commands: https://aquasecurity.github.io/trivy/v0.55/getting-started/installation/)
sudo apt-get install wget apt-transport-https gnupg
wget -qO - https://aquasecurity.github.io/trivy-repo/deb/public.key | gpg --dearmor | sudo tee /usr/share/keyrings/trivy.gpg > /dev/null
echo "deb [signed-by=/usr/share/keyrings/trivy.gpg] https://aquasecurity.github.io/trivy-repo/deb generic main" | sudo tee -a /etc/apt/sources.list.d/trivy.list
sudo apt-get update
sudo apt-get install trivy

verifiy trivy installation: trivy --version
8. Install Docker Scout
Make sure to Login to DockerHub account in browser

Goto MobaXTerm Terminal > Login to DockerHub - > docker login -u <DockerHubUser Name> - Click Enter > Enter the password o DockerHub - > Lets install the Docker Scout --> curl -sSfL https://raw.githubusercontent.com/docker/scout-cli/main/install.sh| sh-s -- -b /ust/local/bin -> Give the permission to dockerScout to execute the file - > sudo chmod 777 /var/run/docker.sock

9. Install SonarQube using Docker
$ docker run -d --name sonar -p 9000:9000 sonarqube:lts-community
$ docker ps (You can see SonarQube container)

