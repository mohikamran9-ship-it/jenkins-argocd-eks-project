

pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'kamran1013/jenkins-argocd-eks-pipeline'
        DOCKER_TAG = 'v1'
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/mohikamran9-ship-it/jenkins-argocd-eks-project.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh '''
                    docker build -t $DOCKER_IMAGE:$DOCKER_TAG .
                '''
            }
        }

        stage('Push to Docker Hub') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub-creds',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]) {
                    sh '''
                        echo "$DOCKER_PASS" | docker login \
                            -u "$DOCKER_USER" --password-stdin

                        docker push $DOCKER_IMAGE:$DOCKER_TAG

                        docker logout
                    '''
                }
            }
        }
    }

    post {
        success {
            echo 'Docker image successfully pushed to Docker Hub!'
        }

        failure {
            echo 'Pipeline failed. Check Console Output.'
        }
    }
}
