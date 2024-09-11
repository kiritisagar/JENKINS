
# 1. Login into AWS Cloud Account
Use your preferred method (AWS Management Console, CLI, etc.) to log in.

# 2. Launch Ubuntu VM Using EC2 Service
AMI: Choose an Ubuntu AMI (e.g., Ubuntu Server 20.04 LTS).
Instance Type: t2.medium

# 3. Connect to vm
Use SSH to connect to your Ubuntu SSH client.

# Install Docker on Ubuntu VM

1.Update the Package Index:
sudo apt update -y

2.Install Docker:
sudo apt install docker.io -y

3.Start the Docker Service:
sudo systemctl start docker

4.Enable Docker to Start at Boot:
sudo systemctl enable docker

6.Add the ubuntu User to the Docker Group:
sudo usermod -aG docker $USER

7.Apply the New Group Membership:
newgrp docker

8.Verify Docker Installation:
docker --version


# Step 2: run sonarqube image

docker run -d --name sonarqube -p 9000:9000 -p 9092:9092 sonarqube:lts-community


## Step-3: Enable 9000 port number in Security Group Inbound Rules & Access Sonar Server

 - URL : http://public-ip:9000/
 - username: admin
 - password:admin 

![image](https://github.com/user-attachments/assets/71d64c56-c225-4cef-bea0-de974f0fedbc)

# Step 4: Manual Create a project ( type Javascript/Typescript)
![image](https://github.com/user-attachments/assets/34f17d5f-d294-4a7b-ba23-77120b36d693)


# Fill you project display name and project key

![image](https://github.com/user-attachments/assets/eea4754a-c1de-4046-ab2d-e29b0935451e)

# Select option “Locally” as image above. You will go to the next page Analyze your project
![image](https://github.com/user-attachments/assets/45c7461a-f46f-4339-a727-8bb797e32c19)

# Click Generate to generate the token of that project

![image](https://github.com/user-attachments/assets/ecfab809-74ad-4520-bd26-aa5e69830adb)



![image](https://github.com/user-attachments/assets/6364cde9-e17c-4af7-87bc-ae8dcc072a71)


