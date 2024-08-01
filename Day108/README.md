![Alt texts](../Images/p1.png)

# DevOps Beginner | Day 108 | Use EC2 Ubuntu Setup Jenkins With User Data ?


```sh
#!/bin/bash
# Update package list
apt update
# Install necessary packages
apt install -y fontconfig openjdk-17-jre
# Verify Java installation
java -version
# Add Jenkins keyring
wget -O /usr/share/keyrings/jenkins-keyring.asc https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key
# Add Jenkins repository to the sources list
echo "deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] https://pkg.jenkins.io/debian-stable binary/" | tee /etc/apt/sources.list.d/jenkins.list > /dev/null
# Update package list again
apt-get update
# Install Jenkins
apt-get install -y jenkins

# Display initial admin password
echo "Initial Admin Password:"
cat /var/lib/jenkins/secrets/initialAdminPassword


```