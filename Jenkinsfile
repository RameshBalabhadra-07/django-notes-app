
@Library("Shared") _

pipeline {
    agent { label "vinod" }

    stages {
        stage("Hello") {
            steps {
                script {
                    hello()
                }
            }
        }

        stage("Code") {
            steps {
                script {
                    clone(
                        "https://github.com/RameshBalabhadra-07/django-notes-app.git",
                        "main"
                    )
                }
            }
        }

        stage("Build") {
            steps {
                script {
                    docker_build("notes-app", "latest", "rameshr28")
                }
            }
        }

        stage("Push to DockerHub") {
            steps {
                script {
                    docker_push("notes-app", "latest","rameshr28")
                }
            }
        }

        stage("Test") {
            steps {
                echo "This is testing code"
            }
        }

        stage("Deploy") {
            steps {
                echo "This is deploying code"
                sh "docker compose down && docker compose up -d --build"
            }
        }
    }
}
