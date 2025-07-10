pipeline {
    agent {
        label 'java-slave'
    }// Run on any available agent

    // Environment variables for configuration
    environment {
        SONAR_SERVER = 'SonarQubeServer1'          // Your SonarQube server name in Jenkins
    }

    stages {

        // Stage 1: Build the application
        stage('Build') {
            tools {
                jdk 'jdk-17'
            }
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
                    sh '''
                    mvn clean verify sonar:sonar \
  -Dsonar.projectKey=pet \
  -Dsonar.host.url=http://34.133.89.244:9000 \
  -Dsonar.login=sqp_fa848e5e27d3e210979de498901a0c464c0b948c
  '''
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
