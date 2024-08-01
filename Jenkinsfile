pipeline {
    agent any
    environment {
        DOCKERHUB_USERNAME = "yasser744"
        APP_NAME = "urlshortener"
        IMAGE_TAG = "${BUILD_NUMBER}"
        IMAGE_NAME = "${DOCKERHUB_USERNAME}/${APP_NAME}"
        REGISTRY_CREDS = 'yasser_dockerhub'
    }
    
    stages {
        stage('Cleanup Workspace') {
            steps {
                script {
                    cleanWs()
                }
            }
        }

        stage('Checkout SCM on github'){
            steps {
                git credentialsId: 'github', 
                url: 'https://github.com/YasserAhmedMoh/testt.git',
                branch: 'main'
            }
        }

            

         stage('Build Docker Image'){
            steps {
                script{
                    docker_image = docker.build "${IMAGE_NAME}"
                }
            }
        }

        

        stage('Push Docker Image To DockerHub') {
            steps {
                script {
                    docker.withRegistry('', REGISTRY_CREDS) {
                        docker_image.push("${BUILD_NUMBER}")
                        docker_image.push('latest')
                    }
                }
            }
        }
    }
}
