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
                         -Dsonar.login=sqp_469df989de78bf4cbc7a028a61cacdb041b1dec0"
                } 
            }
        }
    }
}
