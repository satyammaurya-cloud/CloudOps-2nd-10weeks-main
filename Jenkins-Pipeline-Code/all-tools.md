## ALL TOOLS Setup Script 🚀

This project sets up a complete DevOps environment including CI/CD, containerization, security scanning, and infrastructure tools.

#### 🤖 System Update:
```bash
sudo yum update -y
```

#### 📦 Git
```bash
sudo yum install git -y
```

#### 🤖 Jenkins
```bash
# Java (Required for Jenkins)
sudo yum install fontconfig java-21-openjdk -y

sudo wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/rpm-stable/jenkins.repo
sudo rpm --import https://pkg.jenkins.io/rpm-stable/jenkins.io-2026.key
sudo yum install jenkins -y
sudo systemctl enable jenkins
sudo systemctl start jenkins
```

# 🐳 Docker and Containers Setup
```bash
sudo yum install docker -y
sudo systemctl start docker
sudo systemctl enable docker
sudo usermod -aG docker ec2-user    # Add users to docker group
sudo usermod -aG docker jenkins
newgrp docker                       # Apply group changes (important)

sudo chmod 666 /var/run/docker.sock # Jenkins can run now Docker without restart, but it’s insecure as all users get access.
    #-------OR--------
sudo systemctl restart jenkins      # Jenkins service will not pick the new group permission until you ran this command
```
- SonarQube → Runs code quality analysis service accessible on port 9000  
- Tomcat → Runs Java web applications (WAR files) accessible on port 8089  
```bash
docker run -d --name sonar -p 9000:9000 sonarqube:lts-community
docker run -d --name tomcat -p 8089:8080 tomcat:latest 
```


#### ☸️ Kubectl
```bash
curl -o kubectl https://amazon-eks.s3.us-west-2.amazonaws.com/1.19.6/2021-01-05/bin/linux/amd64/kubectl 
chmod +x kubectl 
sudo mv kubectl /usr/local/bin/
```
#### ⚙️ Eksctl
```bash
curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp 
sudo mv /tmp/eksctl /usr/local/bin 
```
#### 🔍 Trivy
```bash
download and install Trivy RPM:
sudo rpm -ivh https://github.com/aquasecurity/trivy/releases/download/v0.48.3/trivy_0.48.3_Linux-64bit.rpm 
```

#### 📦 Maven
```bash
sudo yum install maven -y
```
#### 📊 SonarQube
```bash
download dependencies:
sudo yum install -y wget nfs-utils 
wget -O /etc/yum.repos.d/sonar.repo http://downloads.sourceforge.net/project/sonar-pkg/rpm/sonar.repo 
yum install sonar -y 
```
#### 📦 JFrog Artifactory
```bash
download repo file:
wget https://releases.jfrog.io/artifactory/artifactory-rpms/artifactory-rpms.repo 
mv artifactory-rpms.repo /etc/yum.repos.d/
yum update -y
yum install jfrog-artifactory-oss -y 
systemctl start artifactory.service 
```
#### 🌍 Terraform
```bash
yum install -y yum-utils
yum-config-manager --add-repo https://rpm.releases.hashicorp.com/AmazonLinux/hashicorp.repo
yum install terraform -y
```


#### 🔄 Terraformer Tool Installation and Usage Example:
```bash
export PROVIDER=all
curl -LO "https://github.com/GoogleCloudPlatform/terraformer/releases/download/$(curl -s https://api.github.com/repos/GoogleCloudPlatform/terraformer/releases/latest | grep tag_name | cut -d '"' -f 4)/terraformer-${PROVIDER}-linux-amd64"
chmod +x terraformer-${PROVIDER}-linux-amd64
sudo mv terraformer-${PROVIDER}-linux-amd64 /usr/local/bin/terraformer
```
