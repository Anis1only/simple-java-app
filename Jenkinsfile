pipeline {
    agent any  // This means the pipeline will run on any available agent

    environment {
        MAVEN_HOME = '/usr/local/maven'  // Adjust this to where Maven is installed on your Jenkins server
    }

    stages {
        // Stage 1: Checkout the code from the repository
        stage('Checkout') {
            steps {
                checkout scm  // This checks out the code from the Git repository
            }
        }

        // Stage 2: Build the project
        stage('Build') {
            steps {
                script {
                    // Running the Maven build command to compile and build the project
                    sh "'$MAVEN_HOME/bin/mvn' clean install -DskipTests=true"
                }
            }
        }

        // Stage 3: Run tests
        stage('Test') {
            steps {
                script {
                    // Running the Maven test command to run unit tests (JUnit or TestNG)
                    sh "'$MAVEN_HOME/bin/mvn' test"
                }
            }
        }

        // Stage 4: Package the application
        stage('Package') {
            steps {
                script {
                    // Running Maven package command to create the .jar or .war file
                    sh "'$MAVEN_HOME/bin/mvn' package"
                }
            }
        }
    }

    // Post actions after the build completes
    post {
        always {
            // Archive the test results (JUnit test reports)
            junit '**/target/test-*.xml'
        }
        success {
            // Notify or take any action on success
            echo 'Build, Test, and Package Succeeded!'
        }
        failure {
            // Notify or take any action on failure
            echo 'Build Failed!'
        }
    }
}
