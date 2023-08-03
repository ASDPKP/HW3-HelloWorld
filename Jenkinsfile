pipeline {
    agent any
    stages {
        stage('Hello') {
            echo 'Hello!!!'
        }

        stage('Create the NGINX namespace') {
            sh 'kubectl create namespace nginx-app-namespace'
        }

        stage('Cleanign the cluster') {
            sh 'kubectl delete deployment nginx-hello-world -n -n nginx-app-namespace'
            sh 'kubectl delete svc nginx-hello-worlds-svc -n nginx-app-namespace'
        }

        stage('Deploying the WebApp to the cluster') {
            sh 'kubectl apply -f webapp-deployment.yaml -n nginx-app-namespace'
        }
    }
}