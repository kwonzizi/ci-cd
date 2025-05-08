pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'kwonzizi/my-app'
        DOCKER_CREDENTIALS_ID = 'kwonzizi_docker'
    }

    stages {

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build(DOCKER_IMAGE)
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', DOCKER_CREDENTIALS_ID) {
                        docker.image(DOCKER_IMAGE).push('latest')
                    }
                }
            }
        }
    }
}
