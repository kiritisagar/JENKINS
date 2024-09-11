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


## sonarqube

pipeline {
    agent any

    tools {
        maven 'maven' // Specify the Maven tool name configured in Jenkins
        // If you have SonarQube Scanner configured, specify it here (optional)
        // sonarQubeScanner 'SonarQube Scanner'
    }

    environment {
        // Specify the SonarQube server details here
        SONAR_HOST_URL = 'http://3.83.43.45:9000/'
        SONAR_AUTH_TOKEN = credentials('sonar') // Replace with your SonarQube token ID
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
        stage('SonarQube Analysis') {
            steps {
                script {
                    // Run SonarQube analysis
                    sh """
                    mvn sonar:sonar \
                    -Dsonar.host.url=${env.SONAR_HOST_URL} \
                    -Dsonar.login=${env.SONAR_AUTH_TOKEN}
                    """
                }
            }
        }
        // Add other stages as needed
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
