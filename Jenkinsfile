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
                        -Dsonar.login=sqp_102653f8646b59eedf7f0b7c0cd5185ebab12ee8"
                } 
            }
        }
        stage ('Dockerbuild_push') {
            steps {
                echo " Buiding the Docker image and pushing it to the DockerHUb Registry"
                sh "docker build -t ${DOCKER_IMAGE}:${DOCKER_TAG} . "
                echo "tag the image "
                sh "docker tag ${DOCKER_IMAGE}   ${DOCKER_REPO}:v1"
                echo " logging into Docker hub"
                sh "docker login -u ${DOCKER_CREDS_USR} -p ${DOCKER_CREDS_PSW}"
                echo "Pushing an image to Docker HUb Registry repo"
                sh  " docker push ${DOCKER_REPO}:v1"
                
            }
        }
    }
}
