pipeline {
    agent {
        label 'java-slave'
    }
    environment {
        SONARQUBE_SERVER = 'SonarQubeServer1'
        DOCKER_REPO = 'cpolina/java-repo2'
    }
    stages {
        stage ('build') {
            steps {
                echo " BUilding an application"
                sh "mvn clean install" 
            }
        }
        stage ('Sonar Analysis') {
            steps {
                echo "Analysis of Project and building a report"
                withSonarQubeEnv("${SONARQUBE_SERVER}") {
                    sh "mvn sonar:sonar -Dsonar.projectKey=spring"
                }
            }
        }
        stage ('Docker build and push') {
            agent {
                label 'docker-slave'
            }
            steps {
                echo "Building an application and pushing an image into Docker hub"
                echo " **************************building an image**********************************"
                sh "docker build -t ${DOCKER_REPO}:${BUILD_NUMBER} -f .devcontainer/Dockerfile . "
                echo " *********************logging into Docker hub****************"
                withCredentials([usernamePassword(credentialsId: 'docker_creds' ,usernameVariable: 'DOCKER_CREDS_USR', passwordVariable: 'DOCKER_CREDS_PSW')]) {
                    sh "echo ${DOCKER_CREDS_PSW} | docker login -u ${DOCKER_CREDS_USR} --passwd-stdin "
                    echo " pushing an image to docker_hub"
                    sh "docker push ${DOCKER_REPO}:${BUILD_NUMBER}"
               }
               sh "docker run -d --name container1  -p 8908:8080  ${DOCKER_REPO}:${BUILD_NUMBER}"
            }
        }
    }
}
