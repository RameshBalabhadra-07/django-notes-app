pipeline {
    agent { label 'vinod' }

    stages {
        stage('Build') {
            steps {
                echo 'Building application'
                sh 'ls'
                sh 'whoami'
                sh 'hostname'
                sh 'whoami'
            }
        }

        stage('Test') {
            steps {
                echo 'Testing application'
            }
        }
    }
}

