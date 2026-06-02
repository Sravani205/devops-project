pipeline {
    agent any

    stages {

        stage('Build Image') {
            steps {
                sh 'docker build -t sravani205/devops-project:$BUILD_NUMBER .'
            }
        }

        stage('Push Image') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub-creds-new',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]) {

                    sh '''
                    echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin
                    docker push sravani205/devops-project:$BUILD_NUMBER
                    '''
                }
            }
        }

        stage('Deploy') {
            steps {
                withEnv(["KUBECONFIG=/var/jenkins_home/.kube/config"]) {
                    sh 'kubectl apply -f deployment.yaml'
                    sh 'kubectl apply -f service.yaml'
                }
            }
        }

    }
}
