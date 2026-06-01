pipeline {
    agent any

    stages {

        stage('Clone') {
            steps {
                git 'YOUR_GITHUB_REPO'
            }
        }

        stage('Build Image') {
            steps {
                sh 'docker build -t username/devops-project:$BUILD_NUMBER .'
            }
        }

        stage('Push Image') {
            steps {
                sh 'docker push username/devops-project:$BUILD_NUMBER'
            }
        }
    }
}
