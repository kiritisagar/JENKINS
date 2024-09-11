# Step-1: Setup Linux VM (Ubuntu)
Login into AWS Cloud Account:
Open the AWS Management Console and log in with your credentials.

# step2:
Launch Ubuntu VM using EC2 Service:

Go to EC2 Dashboard.
Click on Launch Instance.
Choose Ubuntu as the AMI (e.g., Ubuntu Server 22.04 LTS).
Select an instance type, e.g., t2.medium.
Configure instance details, add storage, and configure security group settings (ensure ports 22 for SSH and 8081 for Nexus are open).
Launch the instance and connect to it using SSH or a terminal client like MobaXterm.

# Step-2: Install Docker on Ubuntu VM
# Update the package list
sudo apt update -y

# Install Docker
sudo apt install docker.io -y

# Start Docker service
sudo systemctl start docker

# Enable Docker to start on boot
sudo systemctl enable docker

# Add your user to the Docker group to run Docker commands without sudo
sudo usermod -aG docker $USER

# Verify Docker Installation
docker -v

# step3: Run Nexus by using Docker Image
docker run -d -p 8081:8081 --name nexus sonatype/nexus3

This command runs the Nexus container in detached mode and maps port 8081 on the host to port 8081 in the container.

# Step-4: Enable Port 8081 in Security Group Inbound Rules & Access Nexus Server
Configure Security Group:

Go to the EC2 Dashboard.
Select Security Groups from the left menu.
Find the security group associated with your instance.
Edit inbound rules to allow traffic on port 8081.

# Access Nexus Server:
http://public-ip:8081/
Replace public-ip with your instance's public IP address.

# Step-5: Get Nexus Password from Docker Container

# Find the container ID of the running Nexus container
docker ps

# Access the container
docker exec -it <container-id> /bin/bash

# Display the Nexus admin password
cat /nexus-data/admin.password
Replace <container-id> with the actual ID of the Nexus container obtained from the docker ps command.

# Step-6: Log in to Nexus Server
Log in to Nexus:
Use the URL from Step-6 to open Nexus in a browser.
Log in using the username admin and the password retrieved in Step-7.
This guide provides a clear path to setting up Docker and running a Nexus repository on an Ubuntu VM.


