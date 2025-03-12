pipeline {
    agent any

    environment {
        MAVEN_HOME = '/usr/share/maven'  // Path to your Maven installation (adjust as necessary)
        JAVA_HOME = '/usr/bin/java'    // Path to your JDK installation (adjust as necessary)
    }

    stages {
        stage('Checkout') {
            steps {
                // Pulls the latest code from GitHub
                git branch: 'main', url: 'https://github.com/Anis1only/simple-java-app.git'
            }
        }

        stage('Build') {
            steps {
                // Runs the Maven build
                script {
                    sh "${MAVEN_HOME}/bin/mvn clean install"
                }
            }
        }

        stage('Test') {
            steps {
                // Run unit tests using Maven
                script {
                    sh "${MAVEN_HOME}/bin/mvn test"
                }
            }
        }

        stage('Package') {
            steps {
                // Package the application using Maven (if tests pass)
                script {
                    sh "${MAVEN_HOME}/bin/mvn package"
                }
            }
        }
    }

    post {
        success {
            // Send success notification via email or Slack
            emailext(subject: "Build Successful", body: "The build was successful!", to: "anismullani0@gmail.com")
        }

        failure {
            // Send failure notification via email or Slack
            emailext(subject: "Build Failed", body: "The build has failed. Please check the Jenkins logs.", to: "anismullani0@gmail.com")
        }
    }
}
