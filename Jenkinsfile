pipeline {
    agent any

    stages {
        stage('Clone') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/jenishxe/devops-cicd-demo.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t django-app:latest .'
            }
        }

        stage('Stop Old Container') {
            steps {
                sh 'docker stop django-app || true'
                sh 'docker rm django-app || true'
            }
        }

        stage('Deploy') {
            steps {
                sh 'docker run -d --name django-app --restart=always -p 8000:8000 django-app:latest'
            }
        }
    }

    post {
        success {
            echo 'Deployment successful!'
        }
        failure {
            echo 'Build failed!'
        }
    }
}