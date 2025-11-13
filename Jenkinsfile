pipeline {
    agent any
    environment {
        BUCKET_NAME = 'my-java-artifact-bucket'
        ARTIFACT_NAME = 'spring-petclinic-3.5.0-SNAPSHOT.jar'
        DOCKER_IMAGE_NAME = 'my-java-app-image'
    } 
    stages {
        stage('Build Artifact') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }
        stage('Push Artifact to Bucket') {
            steps {
                sh "gsutil cp target/${ARTIFACT_NAME} gs://${BUCKET_NAME}/"
            }
        }
        stage('Build Docker Image') {
            steps {
                sh "gsutil cp gs://${BUCKET_NAME}/${ARTIFACT_NAME} ."
                sh "docker build -t ${DOCKER_IMAGE_NAME} ."
            }
        }
    }
}
