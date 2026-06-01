pipeline {
    agent any

    stages {


        stage('Build Image') {
            steps {
                sh 'docker build -t Sravani205/devops-project:$BUILD_NUMBER .'
            }
        }

        stage('Push Image') {
            steps {
                sh 'docker push Sravani205/devops-project:$BUILD_NUMBER'
            }
        }
    }
}
