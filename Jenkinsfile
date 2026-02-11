@Library("shared") _
pipeline {
    agent { label "local-agent-1" }

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
                    clone("https://github.com/Preeth02/django-notes-app", "main")
                }
            }
        }

        stage("Build") {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhubCred',
                    usernameVariable: 'USERNAME',
                    passwordVariable: 'PASSWORD'
                )]) {
                    script {
                        docker_build("notes-app", env.USERNAME, "latest")
                    }
                }
            }
        }

        stage("Test") {
            steps {
                echo "Testing..."
            }
        }

        stage("Push to Docker Hub") {
            steps {
                script {
                    docker_push("notes-app","latest")
                }
            }
        }

        stage("Deploy") {
            steps {
                sh "docker compose up -d"
            }
        }

    }  // closes stages

}  // closes pipeline
