
pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/mohikamran9-ship-it/jenkins-argocd-eks-project.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t jenkins-argocd-app:v1 .'
            }
        }
    }
}
