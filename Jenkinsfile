pipeline {
    agent {
        label 'java-slave'
    }
    environment {
        SONARQUBE_SERVER ='SonarQubeServer1'
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
                    sh 'mvn sonar:sonar'
                } 
            }
        }
    }
}

