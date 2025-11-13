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
                script {
                    // Build the Java artifact using Maven
                    sh 'mvn clean package -DskipTests'
                }
            }
        }
        stage('Push Artifact to Bucket') {
            steps {
                // Using withCredentials to handle the GCP service account key
                withCredentials([file(credentialsId: 'gcp-sa-key', variable: 'GCP_KEY')]) {
                    script {
                        // Authenticate and push the artifact to GCS
                        sh '''
                            set -e
                            gcloud auth activate-service-account --key-file=$GCP_KEY
                            gcloud config set project 'gowtham-project-476511'
                            gsutil cp target/${ARTIFACT_NAME} gs://${BUCKET_NAME}/
                        '''
                    }
                }
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    // Download the artifact from GCS and build the Docker image
                    sh "gsutil cp gs://${BUCKET_NAME}/${ARTIFACT_NAME} ."
                    sh "docker build -t ${DOCKER_IMAGE_NAME} ."
                }
            }
        }
    }
}
