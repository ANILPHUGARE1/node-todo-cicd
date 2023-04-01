pipeline {
    agent any;

    stages {
        stage('Pulling Code') {
            steps {
                git credentialsId: 'Git_credential', url: 'https://github.com/ANILPHUGARE1/node-todo-cicd.git' 

            }
        }
        stage('Build Images') {
            steps {
               
                sh 'docker build . -t anilphugare1/nodejs3:v1'
            }
        }
        
        stage('Build & Test') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub_password', passwordVariable: 'docker_password', usernameVariable: 'dockerhub_username')]) {
                    sh "docker login -u ${env.dockerhub_username} -p ${env.docker_password}"
                    sh 'docker push anilphugare1/nodejs3:v1'
                }
            }
        }
        stage('Deploy') {
            steps {
                sh "docker-compose down && docker-compose up -d"
            }
        }
    }
}
