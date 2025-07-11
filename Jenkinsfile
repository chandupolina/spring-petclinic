pipeline {
    agent any
    environment {
        SONARQUBE_SERVER ='SonarQubeServer1'
        DOCKER_REPO = 'cpolina/java_repo'
        DOCKER_IMAGE = 'first_image'
        DOCKER_CREDS = credentials('docker_creds')
    } 
    stages {
        stage ('sonarqube analysis') {
            steps {
                echo "project analysis report"
                sh '''
                mvn clean verify sonar:sonar \
  -Dsonar.projectKey=scanpro \
  -Dsonar.host.url=http://34.133.89.244:9000 \
  -Dsonar.login=sqp_4d839c69c0ae3b38862596c85ec0eef2187e7105 \
  -DskipTests
  '''
                    
                } 
            }
        }
    }
