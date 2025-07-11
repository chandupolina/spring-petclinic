pipeline {
    agent any
    environment {
        SONARQUBE_SERVER ='SonarQubeServer1'
        DOCKER_REPO = 'cpolina/java_repo'
        DOCKER_IMAGE = 'first_image'
        DOCKER_CREDS = credentials('docker_creds')
    } 
    stages {
        stage ('Build') {
            steps {
                echo " Building application "
                sh 'mvn clean install'
            }
        }
        stage ('sonarqube analysis') {
            steps {
                echo "project analysis report"
                withSonarQubeEnv("${SONARQUBE_SERVER}") {
                    sh "mvn clean verify sonar:sonar \
                          -Dsonar.projectKey=spring-petclinic \
                         -Dsonar.host.url=http://34.133.89.244:9000 \
                         -Dsonar.login=sqp_ca0a1e58aea60b32d6748b0d3ee3d415e652d5af"
                } 
            }
        }
    }
}
