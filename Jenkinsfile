pipeline {
    agent any
    environment {
        SONARQUBE_SERVER ='SonarQubeServer1'
        DOCKER_REPO = 'cpolina/java_repo'
        DOCKER_IMAGE = 'first_image'
        DOCKER_CREDS = credentials('docker_creds')
    } 
    stages {
        stage ('Docker build and push') {
            steps {
                echo " building an image "
                sh "docker build -t  ${DOCKER_IMAGE} -f .Devcontainer/Dockerfile "
                echo  " tags an image means renaming the image "
                sh "docker tag ${DOCKER_IMAGE}:latest  ${DOCKER_REPO}/${DOCKER_IMAGE}:${BUILD_NUMBER}"
                echo "*******************************docker login *************************"
                sh "docker login -u ${DOCKER_CREDS_USR} -p ${DOCKER_CREDS_PSW}"
                echo "*************************pushing image to registry******************************"
                sh "docker push ${DOCKER_REPO}/${DOCKER_IMAGE}:${BUILD_NUMBER}"
            }
        }
    }
}
