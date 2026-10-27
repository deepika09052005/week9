pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                bat 'docker build -t deepika09052005/week9-registration:latest .'
            }
        }

        stage('Push') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub-creds',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]) {
                    bat 'docker login -u "%DOCKER_USER%" -p "%DOCKER_PASS%"'
                    bat 'docker push deepika09052005/week9-registration:latest'
                }
            }
        }

        stage('Deploy') {
            steps {
                bat 'kubectl apply -f deployment.yaml'
                bat 'kubectl apply -f service.yaml'
            }
        }
    }
}