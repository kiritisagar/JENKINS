Integrating Jenkins with Nexus Repository Manager allows you to automate the process of deploying your build artifacts (e.g., JAR, WAR files) to a Nexus repository. This is useful for managing and distributing your artifacts within your organization or for external clients. Here’s how to integrate Nexus with Jenkins:

### **Step 1: Set Up Nexus Repository**
1. **Install Nexus Repository Manager:**
   - Download and install Nexus Repository Manager OSS or Nexus Repository Pro from the [official website](https://www.sonatype.com/products/repository-oss).
   - Start Nexus and configure it according to your environment.

2. **Create a Maven Repository in Nexus:**
   - Log in to Nexus Repository Manager.
   - Go to `Repositories` > `Create Repository`.
   - Select `maven2 (hosted)` for a hosted Maven repository.
   - Configure the repository (e.g., name, deployment policy) and click `Create repository`.

3. **Create a User with Deployment Privileges:**
   - Go to `Security` > `Users` > `Create user`.
   - Create a user with the necessary roles (e.g., `nx-deploy`) to allow Jenkins to deploy artifacts to the Nexus repository.

### **Step 2: Install and Configure Jenkins Plugins**
1. **Install the Nexus Artifact Uploader Plugin:**
   - Go to Jenkins Dashboard > `Manage Jenkins` > `Manage Plugins`.
   - Under the `Available` tab, search for `Nexus Artifact Uploader`.
   - Install the plugin.

2. **Configure Jenkins to Use Nexus Credentials:**
   - Go to Jenkins Dashboard > `Manage Jenkins` > `Manage Credentials`.
   - Under the appropriate domain (e.g., `Global`), click `Add Credentials`.
   - Choose `Username with password` and enter the Nexus username and password that you created earlier.
   - Give the credentials an ID (e.g., `nexus-creds`) for easy reference in your Jenkins jobs.

### **Step 3: Create a Jenkins Job to Deploy Artifacts to Nexus**
1. **Create a New Maven Project:**
   - Go to Jenkins Dashboard > `New Item`.
   - Enter a name for your project (e.g., `My-Maven-Nexus-Project`).
   - Select `Maven Project` and click `OK`.

2. **Configure Source Code Management:**
   - Under `Source Code Management`, select `Git` and enter the repository URL.

3. **Configure Build Goals:**
   - In the `Build` section, enter the Maven goals, e.g., `clean package`.
   - You can also add other Maven phases if needed, like `install`.

4. **Add Post-Build Action to Deploy to Nexus:**
   - Scroll down to the `Post-build Actions` section.
   - Select `Nexus Artifact Uploader`.
   - **Repository URL:** Enter your Nexus repository URL (e.g., `http://<nexus-url>:8081/repository/maven-releases/`).
   - **Credentials:** Select the credentials ID (`nexus-creds`) you configured earlier.
   - **Group ID, Artifact ID, Version:** Specify these details to define the artifact in Nexus.
   - **Artifact File:** Specify the path to the artifact you want to upload, e.g., `target/*.jar` or `target/*.war`.
   - **Packaging:** Specify the packaging type, such as `jar` or `war`.
   - **Repository:** Choose the Nexus repository name where you want to deploy your artifacts.

5. **Save and Run the Job:**
   - Click `Save` to store the configuration.
   - Click `Build Now` to trigger the build and deploy the artifact to Nexus.

### **Step 4: Verify the Deployment in Nexus**
1. Log in to Nexus Repository Manager.
2. Go to the `Browse` section and select the repository where you deployed the artifact.
3. Confirm that the artifact (e.g., JAR or WAR file) has been uploaded and is available for download.

### **Example: Jenkins Pipeline with Nexus Integration**
If you are using Jenkins Pipeline (Jenkinsfile), here’s an example to integrate with Nexus:

```groovy
pipeline {
    agent any

    tools {
        maven 'Maven 3.8.1'
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/user/repository.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Upload to Nexus') {
            steps {
                nexusArtifactUploader artifacts: [[artifactId: 'my-artifact-id',
                                                  classifier: '',
                                                  file: 'target/my-artifact.jar',
                                                  type: 'jar']],
                                      credentialsId: 'nexus-creds',
                                      groupId: 'com.example',
                                      nexusUrl: 'http://<nexus-url>:8081',
                                      nexusVersion: 'nexus3',
                                      protocol: 'http',
                                      repository: 'maven-releases',
                                      version: '1.0.0'
            }
        }
    }

    post {
        always {
            junit 'target/surefire-reports/*.xml'
            archiveArtifacts artifacts: '**/target/*.jar', allowEmptyArchive: true
        }
    }
}
```

### **Key Points:**
- **Maven Goals:** Customize your Maven goals based on your project needs.
- **Nexus Configuration:** Ensure the Nexus repository and credentials are correctly configured in Jenkins.
- **Artifact Upload:** Ensure that the correct artifact path and details are specified in the `Nexus Artifact Uploader` step.

By following these steps, you’ll be able to integrate Jenkins with Nexus, allowing you to automate the deployment of your build artifacts to your Nexus repository.
