pipeline {
    agent any // Run on any available agent

    // Environment variables for configuration
    environment {
        SONAR_SERVER = 'SonarQubeServer1'          // Your SonarQube server name in Jenkins
    }

    stages {

        // Stage 1: Build the application
        stage('Build') {
            steps {
                echo 'Building the application...'
                // Replace with your build command (e.g., 'npm install')
                sh 'mvn clean package -Dmaven.test.skip=true'
            }
        }


        // Stage 2: Scan with SonarQube
        stage('SonarQube Scan') {
            steps {
                echo 'Running SonarQube analysis...'
                // Sets up SonarQube environment
                withSonarQubeEnv(SONAR_SERVER) {
                    // Runs the scanner
                    sh 'mvn sonar:sonar'
                }
            }
        }
    }

    // Runs after the pipeline finishes
    post {
        always {
            echo 'Pipeline finished.'
            cleanWs() // Clean up the workspace
        }
    }
}
