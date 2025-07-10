pipeline {
    agent {
        label 'java-slave'
    }// Run on any available agent

    // Environment variables for configuration
    stages {

        // Stage 1: Build the application
        stage('Build') {
            tools {
                jdk 'jdk-17'
            }
            steps {
                echo 'Building the application...'
                git clone https://github.com/chandupolina/spring-petclinic.git
                // Replace with your build command (e.g., 'npm install')
                dir('spring-petclinic.git'){
                    sh '''
                    mvn clean verify sonar:sonar \
                      -DskipTests\
                      -Dsonar.projectKey=pet \
                      -Dsonar.host.url=http://34.133.89.244:9000 \
                       -Dsonar.login=sqp_fa848e5e27d3e210979de498901a0c464c0b948c
                       ''' 
                }
            }
        }


        // Stage 2: Scan with SonarQube
    }

    // Runs after the pipeline finishes
    post {
        always {
            echo 'Pipeline finished.'
            cleanWs() // Clean up the workspace
        }
    }
}
