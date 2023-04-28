pipeline {
    agent { label 'dev' }
    stages{
        stage('code'){
            steps{
                git url: 'https://github.com/oppo-A5/node-todo-cicd.git', branch: 'master'
            }
        }
        stage('build'){
            steps{
                sh 'docker build . -t nikmeshram/node-todo-app-cicd:latest'
            }
        }
        stage('login and push image'){
            steps{
                echo 'loging into docker hub and pushing image'
                withCredentials([usernamePassword('credentialsId': 'dockerhub', 'passwordVariable':'dockerHUBPassword', 'usernameVariable':'dockerHUBUser')]) {
                    sh "docker login -u ${env.dockerHUBUser} -p ${env.dockerHUBPassword}"
                    sh "docker push nikmeshram/node-todo-app-cicd:latest"
                }
            }
        }
        stage('deploy'){
            steps{
                sh 'docker-compose down && docker-compose up -d'
            }
        }
    }
}
