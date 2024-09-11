Step 1: Install the SonarQube Scanner Plugin in Jenkins
Go to Jenkins Dashboard.
Click on Manage Jenkins > Manage Plugins.
Go to the Available tab and search for SonarQube Scanner.
Install the SonarQube Scanner plugin.
Step 2: Configure SonarQube in Jenkins
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
Step 3: Configure SonarQube Scanner in Jenkins
Go to Jenkins Dashboard.
Click on Manage Jenkins > Global Tool Configuration.
Scroll down to the SonarQube Scanner section.
Click Add SonarQube Scanner.
Provide a name and choose the installation method:
Automatic installation (Jenkins will download and install the scanner).
Manual installation (provide the path to the SonarQube scanner if already installed).
Click Save.
Step 4: Add SonarQube Analysis to Jenkins Job
Go to the Jenkins Dashboard.

Open the job where you want to add SonarQube analysis.

Click on Configure.

In the Build Environment section, check Prepare SonarQube Scanner environment.

In the Build section, click Add build step and select Invoke SonarQube Scanner.

Configure the SonarQube Scanner:

Analysis properties: Add the analysis properties like sonar.projectKey, sonar.sources, etc.
Example properties:
plaintext
Copy code
sonar.projectKey=my-project-key
sonar.sources=src
sonar.java.binaries=target/classes
If you have a sonar-project.properties file in your project, this step might be optional as the scanner will automatically use it.
Click Save.

Step 5: Trigger the Build
Go back to your Jenkins job.
Click Build Now.
Jenkins will run the build and execute the SonarQube analysis as part of the pipeline.
Step 6: View SonarQube Results
Once the build completes, you can see the SonarQube results directly in the SonarQube dashboard.
Jenkins will also provide a link to the SonarQube dashboard in the build logs if the integration is correctly configured.
Example Jenkins Pipeline Script (Declarative Pipeline)
If you're using a Jenkins Pipeline (Jenkinsfile), here's an example:

groovy
Copy code
pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('My SonarQube Server') {
                    sh 'mvn sonar:sonar'
                }
            }
        }
        stage("Quality Gate") {
            steps {
                timeout(time: 1, unit: 'HOURS') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }
    }
}
Notes:
Replace 'My SonarQube Server' with the name of your SonarQube server configured in Jenkins.
The waitForQualityGate step will wait for the SonarQube analysis to complete and will fail the build if the quality gate fails.
