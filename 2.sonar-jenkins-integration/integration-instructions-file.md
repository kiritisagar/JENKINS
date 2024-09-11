
![image](https://github.com/user-attachments/assets/abdbd7b0-e750-4dc6-ad65-91a0c2e2599c)

## in sonar-server
# step1: Create a New Project:
Once logged in, you need to create a new project in SonarQube. Follow these steps:

Click on the “Projects” tab on the top menu.
Click on the “Create Project” button.
Provide a unique project key and a display name for your project.
Choose the appropriate language for your project. SonarQube supports various programming languages.
Click on “Set Up” to proceed.

# Generate SonarQube Token for auth of jenkins
Log in to SonarQube using the admin credentials.
Navigate to “My Account” -> “Security” -> “Generate Tokens”.
Provide a name for the token and click on “Generate”. Save the generated token securely.



#### in jenkins server
# step2:To set up SonarQube credentials in Jenkins:
Go to “Manage Jenkins” > “Manage Credentials”.
Choose the appropriate domain.
Click “Add Credentials”.
Select the credential type (e.g., “Secret text” for tokens, “Username with password” for username/password).
Enter the credential details.
Provide an ID and description.
Save the credentials.

![Screenshot (213)](https://github.com/user-attachments/assets/544ccc13-9ee2-47a9-be6e-7c9a91bfccb1)
![Screenshot (214)](https://github.com/user-attachments/assets/48cd16a8-56f7-4490-b310-151489f11346)

# Step 3: Install the SonarQube Scanner Plugin in Jenkins
Go to Jenkins Dashboard.
Click on Manage Jenkins > Manage Plugins.
Go to the Available tab and search for SonarQube Scanner.
Install the SonarQube Scanner plugin.

# Step 2: Configure SonarQube in Jenkins
Go to Jenkins Dashboard.
Click on Manage Jenkins > Configure System.
Scroll down to the SonarQube servers section.
Click Add SonarQube.
Provide a name for your SonarQube server.
Enter the Server URL (e.g., http://localhost:9000).
If authentication is required, add the SonarQube token:
Generate a token in SonarQube by going to My Account > Security > Generate Tokens.
In Jenkins, under the Server authentication token section, click Add and enter the token.
Click Save to store the configuration.

![image](https://github.com/user-attachments/assets/d55c740e-6d50-4c60-828f-5308941ce3f0)

# Step 4: Add SonarQube Analysis to Jenkins Job
Go to the Jenkins Dashboard.
Open the job where you want to add SonarQube analysis.
Click on Configure.
In the Build Environment section, check Prepare SonarQube Scanner environment.
In the Build section, click Add build step and select Invoke SonarQube Scanner.

# Configure the SonarQube Scanner:

![Screenshot (216)](https://github.com/user-attachments/assets/987934c7-2023-4267-af39-66131862302f)

![Screenshot (215)](https://github.com/user-attachments/assets/4ee0c4d9-168d-45bb-8c72-05567a4cd8ae)


# Once the SonarQube stage executes, check the SonarQube dashboard (http://sonarip:9000) for the analysis report.
![image](https://github.com/user-attachments/assets/333565c8-5b2a-4e9b-9285-3ee83144369b)

