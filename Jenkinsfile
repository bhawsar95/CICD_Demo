pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "abhishekf5/ultimate-cicd:${BUILD_NUMBER}"
    }

    stages {
        stage('Build and Push Docker Image') {
            steps {
                script {
                    // Build the Docker image
                    sh 'cd java-maven-sonar-argocd-helm-k8s/spring-boot-app && docker build -t ${DOCKER_IMAGE} .'

                    // Log in to Docker Hub using an access token
                    withCredentials([string(credentialsId: 'docker-cred', variable: 'DOCKER_ACCESS_TOKEN')]) {
                        sh "docker login -u bhawsarshubham95 -p ${dckr_pat_RoEUUmoJFz_fO1mJnmIw0-QaZww}"
                    }

                    // Push the Docker image
                    sh 'docker push ${DOCKER_IMAGE}'
                }
            }
        }
    }

    post {
        always {
            // Clean up Docker containers
            cleanWs()
            script {
                // Remove the Docker image
                sh 'docker rmi ${DOCKER_IMAGE}'
            }
        }
    }
}
