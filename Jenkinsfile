pipeline {
    agent any

    stages {


        stage('Build Image') {
            steps {
                sh 'docker build -t sravani205/devops-project:v$BUILD_NUMBER .'
            }
        }

        stage('Push Image') {
            steps {
                sh 'docker push sravani205/devops-project:v$BUILD_NUMBER'
            }
        }
        stage('Deploy') {
            steps {
             sh 'kubectl apply -f deployment.yaml'
             sh 'kubectl apply -f service.yaml'
    }
}
}
}
