pipeline {
    agent any

    stages {
        stage('Clone repository') {
            steps {
                checkout scm
            }
        }

        stage('Build image') {
            steps {
                script {
                    // Build the Docker image
                    docker.build("emilijalakinska/kiii-jenkins")
                }
            }
        }

        stage('Push image') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
                        // Push the image to Docker Hub
                        def customTag = "${env.BRANCH_NAME}-${env.BUILD_NUMBER}"
                        docker.image("emilijalakinska/kiii-jenkins").push(customTag)
                        docker.image("emilijalakinska/kiii-jenkins").push("${env.BRANCH_NAME}-latest")
                    }
                }
            }
        }
    }
}