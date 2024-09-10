# Step - 1 : Create Linux VM
Create Ubuntu VM using AWS EC2 (t2.medium)
Enable 8080 Port Number in Security Group Inbound Rules
Connect to VM using MobaXterm

# Step-2 : Instal Java
sudo apt update
sudo apt install fontconfig openjdk-17-jre
java -version

# Step-3 : Install Jenkins
sudo wget -O /usr/share/keyrings/jenkins-keyring.asc \
  https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update
sudo apt-get install jenkins

# Step-4 : Start Jenkins
sudo systemctl enable jenkins
sudo systemctl start jenkins
Verify Jenkins
sudo systemctl status jenkins

# Step-6 : Open jenkins server in browser using VM public ip
http://public-ip:8080/
sudo cat /var/lib/jenkins/secrets/initialAdminPassword


![image](https://github.com/user-attachments/assets/d8186853-c879-4f41-a0ea-21e5714de592)


# step-7:

go witht suggested plugin
![image](https://github.com/user-attachments/assets/5878f33b-608e-40f9-8dfe-75e4c28bff2a)


# step-8:
Set Up user

![image](https://github.com/user-attachments/assets/5adb10ac-e545-41ad-b2fe-85312de51a44)

# It’s ready
![image](https://github.com/user-attachments/assets/3f33ddad-e90a-40dd-90c8-4a6385b01014)
