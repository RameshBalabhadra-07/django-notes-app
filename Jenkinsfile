
pipeline {
    agent { label 'vinod' }

    stages {
        stage('Build') {
            steps {
                echo 'Building application'
                sh 'hostname'
                sh 'docker build -t notes-app:latest .'
            }
        }

        stage('Test') {
            steps {
                echo 'Testing Docker image'
                sh 'docker image inspect notes-app:latest'
                sh 'docker run -d --name notes-test -p 8001:8000 notes-app:latest'
            }
        }
    }
}
