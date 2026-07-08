pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t flask-cd-demo-ab .'
            }
        }

        stage('Login to ECR') {
            steps {
                sh '''
                aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 992382545251.dkr.ecr.us-east-1.amazonaws.com
                '''
            }
        }

        stage('Tag Image') {
            steps {
                sh 'docker tag flask-cd-demo-ab:latest 992382545251.dkr.ecr.us-east-1.amazonaws.com/flask-cd-demo-ab:latest'
            }
        }

        stage('Push Image') {
            steps {
                sh 'docker push 992382545251.dkr.ecr.us-east-1.amazonaws.com/flask-cd-demo-ab:latest'
            }
        }
    }
}
