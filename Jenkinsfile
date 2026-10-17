
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

                echo 'Waiting for Django to become healthy'
                sh '''
                    for i in $(seq 1 30); do
                        status=$(docker inspect --format='{{.State.Health.Status}}' django_cont 2>/dev/null || true)

                        if [ "$status" = "healthy" ]; then
                            echo "Django is healthy"
                            exit 0
                        fi

                        if [ "$status" = "unhealthy" ]; then
                            echo "Django is unhealthy"
                            docker compose logs --tail=50 django_app
                            exit 1
                        fi

                        if [ "$i" -eq 30 ]; then
                            echo "Django did not become healthy in time"
                            docker compose logs --tail=50 django_app
                            exit 1
                        fi

                        sleep 5
                    done
                '''

                sh 'docker compose ps'
            }
        }

        stage('Smoke Test') {
            steps {
                echo 'Checking Nginx HTTP response'
                sh '''
                    code=$(curl -sS -o /dev/null -w '%{http_code}' http://localhost/)
                    echo "Nginx HTTP status: $code"
                    test "$code" = "200"
                    echo 'successfully completed the test'
                '''
            }
        }
    }
}
