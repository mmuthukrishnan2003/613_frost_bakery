pipeline {
    agent any

    environment {
        IMAGE_NAME = "613-frost-bakery"
        CONTAINER_NAME = "613_frost_bakery"
        PORT = "30351"
        DOCKER_CREDS = credentials('docker-cred')
    }

    stages {

        stage('Build Docker Image') {
            steps {
                sh "docker build -t ${IMAGE_NAME}:v1 ."
            }
        }

        stage('Login to Docker Hub') {
            steps {
                sh "echo ${DOCKER_CREDS_PSW} | docker login -u ${DOCKER_CREDS_USR} --password-stdin"
            }
        }

        stage('Tag Image') {
            steps {
                sh "docker tag ${IMAGE_NAME}:v1 ${DOCKER_CREDS_USR}/${IMAGE_NAME}:v1"
            }
        }

        stage('Push Image') {
            steps {
                sh "docker push ${DOCKER_CREDS_USR}/${IMAGE_NAME}:v1"
            }
        }

        stage('Stop Old Container') {
            steps {
                sh "docker rm -f ${CONTAINER_NAME} || true"
            }
        }

        stage('Run Container') {
            steps {
                sh """
                docker run -d -p ${PORT}:80 \
                --name ${CONTAINER_NAME} \
                ${DOCKER_CREDS_USR}/${IMAGE_NAME}:v1
                """
            }
        }
    }
}
