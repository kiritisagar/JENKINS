Integrating Maven with Jenkins allows you to automate the build and testing processes for your Java projects. Here's how to integrate Maven with Jenkins:

### **Step 1: Install Jenkins and Maven**
1. **Jenkins Installation:**
   - Ensure Jenkins is installed and running on your system. You can download and install it from the [official Jenkins website](https://www.jenkins.io/download/).
  
2. **Maven Installation:**
   - Install Maven on the machine where Jenkins is running. You can download Maven from the [Apache Maven website](https://maven.apache.org/download.cgi) and follow the installation instructions.
   - Alternatively, you can install Maven directly through Jenkins, which will be covered later.

### **Step 2: Install the Maven Plugin in Jenkins**
1. Go to the Jenkins Dashboard.
2. Click on `Manage Jenkins` > `Manage Plugins`.
3. Go to the `Available` tab and search for `Maven Integration Plugin`.
4. Install the `Maven Integration Plugin`.

![image](https://github.com/user-attachments/assets/d943dd3d-8b81-4c6e-997c-de24d2cb2972)
![image](https://github.com/user-attachments/assets/79d59b42-6c4d-4045-9efa-a408718182c9)
![image](https://github.com/user-attachments/assets/c906ea38-9f7c-4948-b3c3-aeca3bb15af7)

### **Step 3: Configure Maven in Jenkins**
1. Go to Jenkins Dashboard.
2. Click on `Manage Jenkins` > `Global Tool Configuration`.
3. Scroll down to the `Maven` section.
4. Click `Add Maven`.
   - **Automatic installation:** Check `Install automatically` and select the version of Maven you want Jenkins to install and use.
   - **Manual installation:** Provide a name and specify the Maven installation path if you have Maven installed on the machine.
5. Click `Save` to store the configuration.

### **Step 4: Create a Maven Job in Jenkins**
1. Go to Jenkins Dashboard.
2. Click on `New Item`.
3. Enter a name for your job (e.g., `My-Maven-Project`).
4. Select `Maven Project` and click `OK`.

### **Step 5: Configure the Maven Job**
1. In the job configuration page, scroll down to the `Source Code Management` section.
   - Select `Git`, `Subversion`, or any other relevant source code management system.
   - Enter the repository URL and any required credentials.

2. In the `Build` section, configure the Maven goals.
   - For a standard Maven build, enter `clean install` in the `Goals and options` field.
   - If you want to skip tests, use `clean install -DskipTests`.

### **Example: Jenkins Pipeline with Maven (Declarative Pipeline)**
If you prefer to use a Jenkins Pipeline (Jenkinsfile), here’s an example:

```groovy
pipeline {
    agent any

    tools {
        maven 'Maven 3.8.1' // Name of Maven installation in Jenkins
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/user/repository.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean install'
            }
        }
    }
}
```
