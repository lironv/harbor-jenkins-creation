
pipeline {
    agent any

    environment {
        DOCKER_REGISTRY = "core.harbor.domain"
        DOCKER_REGISTRY_USER = credentials('admin')
        DOCKER_REGISTRY_PASSWORD = credentials('nJIQqYVVQh')
        IMAGE_NAME = "own-image"
        IMAGE_TAG = "latest"
        DOCKERFILE_PATH = "./Dockerfile"
    }

    stages {

        stage('Build Docker Image') {
            steps {
                git branch: 'main', url: 'https://github.com/lironv/binom-print-pipeline.git'

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
