pipeline {
    agent any
    stages {
        stage(' GitHub') {
            steps {
                git 'https://github.com/naveenleon/Mazeball.git'
            }
        }
        stage('Build the Docker image') {
            steps {
                sh 'sudo docker build -t naveenleon/home/vijay/workspace/game-project'
                sh 'sudo docker tag naveenleon /mazeimage:latest'
                sh 'sudo docker tag naveenleon vijay3639/mazeimage:${BUILD_NUMBER}'
            }
        }
        stage('Push the Docker image') {
            steps {
                sh 'sudo docker image push vijay3639/mazeimage:latest'
                sh 'sudo docker image push vijay3639/mazeimage:${BUILD_NUMBER}'
            }
        }
        stage('Deploy on Kubernetes') {
            steps {
                sh 'sudo kubectl apply -f /home/vijay/workspace/game-project/pod.yml'
                sh 'sudo kubectl rollout restart deployment loadbalancer-pod'
            }
        }
    }
}
