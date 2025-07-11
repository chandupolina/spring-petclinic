pipeline {
    agent any
    environment {
        SONARQUBE_SERVER = 'SonarQubeServer1'
        DOCKER_REPO = 'cpolina/java_repo'
        DOCKER_IMAGE = 'first_image'
        DOCKER_CREDS = credentials('docker_creds')
    } 
    stages {
        stage('Docker Build and Push') {
            steps {
                script {
                    echo "Cleaning up Docker environment"
                    sh "docker system prune -a -f --volumes || true"
                    sh "docker builder prune -f || true"
                    
                    echo "Checking disk space"
                    sh "df -h"
                    
                    echo "Building Docker image without tag"
                    sh "docker build -t ${DOCKER_IMAGE} -f .devcontainer/Dockerfile ."
                    
                    echo "Tagging Docker image for Docker Hub"
                    sh "docker tag ${DOCKER_IMAGE}:latest ${DOCKER_REPO}:${BUILD_NUMBER}"
                    
                    echo "Logging into Docker Hub"
                    sh "echo ${DOCKER_CREDS_PSW} | docker login -u ${DOCKER_CREDS_USR} --password-stdin"
                    
                    echo "Pushing image to Docker Hub"
                    sh "docker push ${DOCKER_REPO}:${BUILD_NUMBER}"
                    
                }
            }
        }
    }
    post {
        always {
            echo "Logging out of Docker Hub"
            sh 'docker logout'
        }
    }
}
