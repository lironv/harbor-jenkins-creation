
pipeline {
    agent any

    environment {
        DOCKER_REGISTRY = "harbor.example.com"
        DOCKER_REGISTRY_USER = credentials('harbor-user')
        DOCKER_REGISTRY_PASSWORD = credentials('harbor-password')
        IMAGE_NAME = "own-image"
        IMAGE_TAG = "latest"
        DOCKERFILE_PATH = "./Dockerfile"
    }

    stages {
        stage('Checkout Git Repo') {
            steps {
                git 'https://github.com/lironv/harbor-jenkins-creation.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.withRegistry(DOCKER_REGISTRY, DOCKER_REGISTRY_USER, DOCKER_REGISTRY_PASSWORD) {
                        def customImage = docker.build("${DOCKER_REGISTRY}/${IMAGE_NAME}:${IMAGE_TAG}", "--file ${DOCKERFILE_PATH} .")
                        customImage.push()
                    }
                }
            }
        }
    }
}
