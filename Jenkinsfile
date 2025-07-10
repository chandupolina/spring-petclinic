pipeline {
    agent any
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
                    sh "mvn clean verify sonar:sonar \
                        -Dsonar.login=sqp_102653f8646b59eedf7f0b7c0cd5185ebab12ee8"
                } 
            }
        }
    }
}
