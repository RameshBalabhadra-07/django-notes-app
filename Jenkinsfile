
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
                echo 'Testing application'
            }
        }
    }
}
