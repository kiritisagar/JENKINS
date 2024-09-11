# git clone:
  
pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Clone code from the specified Git repository
                git branch: 'main', url: 'https://github.com/kiritisagar/JENKINS.git'
            }
        }
    }
}


## maven build ##

pipeline {
    agent any

    tools {
        maven 'maven' // Specify the Maven tool name configured in Jenkins
    }

    stages {
        stage('Checkout') {
            steps {
                // Clone code from the specified Git repository
                git branch: 'main', url: 'https://github.com/kiritisagar/JENKINS.git'
            }
        }
        stage('Build') {
            steps {
                script {
                    // Run Maven install with skipTests
                    sh 'mvn clean install -DskipTests'
                }
            }
        }
        // Add other stages as needed
    }
}
