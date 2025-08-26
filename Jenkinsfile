pipeline {
    agent any
    environment {
        IMAGE = "thirumurugan133/devops-simple:${BUILD_NUMBER}"
    }

    stages {
        stage('Clone Repo') {
            steps {
                git branch: 'main', url: 'https://github.com/thiru817/simple-devops-project.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build('thiru817/simple-devops-project')
                }
            }
        }

        stage('Push to DockerHub') {
            steps {
                withDockerRegistry(credentialsId: 'dockerhub-creds', url: '') {
                    script {
                        docker.image('thiru817/simple-devops-project').push()
                    }
                }
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sh 'kubectl apply -f deployment.yaml'
                sh 'kubectl apply -f service.yaml'
            }
        }
    }
}
