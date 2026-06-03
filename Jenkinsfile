pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                    credentialsId: 'Git-cred',
                    url: 'https://github.com/gopinathbca35/Simplybyte_calculator.git'
            }
        }

        stage('Docker Build') {
            steps {
                bat 'docker build -t calculator:latest .'
            }
        }

        stage('Docker Tag') {
            steps {
                bat 'docker tag calculator:latest gopinathbca35/calculator-app:latest'
            }
        }

        stage('Docker Push') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub-creds',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]) {

                    bat '''
                    docker login -u %DOCKER_USER% -p %DOCKER_PASS%
                    docker push gopinathbca35/calculator-app:latest
                    '''
                }
            }
        }
    }
}