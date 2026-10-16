
pipeline {
    agent { label 'vinod' }

    stages {
        stage('Code') {
            steps {
                echo 'Checking source code'
                sh 'pwd'
                sh 'ls -la'
            }
        }

        stage('Build') {
            steps {
                echo 'Building Docker images'
                sh 'docker compose build'
            }
        }

        stage('Test') {
            steps {
                echo 'Validating Docker images'
                sh 'docker image inspect django_app'
                sh 'docker compose config --quiet'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying application'
                sh 'docker compose up -d'
                sh 'docker compose ps'
            }
        }
    }
}
