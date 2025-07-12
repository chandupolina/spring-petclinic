pipeline {
    agent any
    environment {
        SONARQUBE_SERVER = 'SonarQubeServer1'
        DOCKER_REPO = 'cpolna/java-repo1'
        DOCKER_IMAGE = 'second_image'
    }
    stages {
        stage ('Sonar Analysis') {
            steps {
                echo "Analysis of Project and building a report"
                withSonarQubeEnv("${SONARQUBE_SERVER}") {
                    sh "mvn clean verify sonar:sonar"
                }
            }
        }
    }
}
