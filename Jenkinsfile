@Library("shared") _
pipeline {
    agent {label "local-agent-1"}
        
    stages {
        stage("Hello"){
            steps{
            script{
                hello()
                }
                }
        }
        stage('Code') {
            steps {
                script{
                clone("https://github.com/Preeth02/django-notes-app", "main")
                }
            }
        }
        stage('Build') {
            steps {
                script{
                    docker_build("notes-app","${USERNAME}","latest");
                }
                // echo 'This is a build stage'
                // sh "docker build -t preetham02/notes-app:latest ."
            }
        }
        stage('Test') {
            steps {
                echo 'This is a test stage'
                echo 'This is a test stage for SCM'
                echo 'This is a test stage for SCM 2'
            }
        }
        stage("Push to docker hub"){
            steps{
                script{
                    docker_push("notes-app","latest")
                }
                // withCredentials([usernamePassword(credentialsId: 'dockerhubCred', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                // sh "docker login -u ${env.USERNAME} -p ${env.PASSWORD}"
                // sh "docker image tag notes-app:latest ${env.USERNAME}/notes-app:latest"
                // sh "docker push ${env.USERNAME}/notes-app:latest"

                }
            }
        }
        stage('Deploy') {
            steps {
                echo 'This is a deploy stage'
                // sh "docker run -d -p 8000:8000 notes-app:latest"
                sh "docker compose up -d"
            }
        }
        }
}
