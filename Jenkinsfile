pipeline {
    agent any;

    stages {
        stage('Pulling Code') {
            steps {
                git url: 'https://github.com/ANILPHUGARE1/node-todo-cicd.git', branch: 'master' 

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
