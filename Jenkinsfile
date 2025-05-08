pipeline {
    agent any

    environment {
        dockerHubRegistry = "kwonzizi/my-app"                   // DockerHub 이미지 이름
        dockerHubRegistryCredential = "kwonzizi_docker"         // Jenkins Credentials ID
    }

    stages {
        stage('docker image build') {
            steps {
                sh "docker build . -t ${dockerHubRegistry}:${currentBuild.number} -t ${dockerHubRegistry}:latest"
            }
            post {
                failure {
                    echo 'Docker image build failure!'
                }
                success {
                    echo 'Docker image build success!'
                }
            }
        }

        stage('Docker Image Push') {
            steps {
                withDockerRegistry([ credentialsId: dockerHubRegistryCredential, url: "" ]) {
                    sh "docker push ${dockerHubRegistry}:${currentBuild.number}"
                    sh "docker push ${dockerHubRegistry}:latest"
                    sleep 10
                }
            }
            post {
                failure {
                    echo 'Docker Image Push failure!'
                    sh "docker rmi ${dockerHubRegistry}:${currentBuild.number} || true"
                    sh "docker rmi ${dockerHubRegistry}:latest || true"
                }
                success {
                    echo 'Docker image push success!'
                    sh "docker rmi ${dockerHubRegistry}:${currentBuild.number} || true"
                    sh "docker rmi ${dockerHubRegistry}:latest || true"
                }
            }
        }
    }
}
