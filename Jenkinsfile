pipeline {
    agent any
    environment {
        docker_creds = credentials('docker-credentials')
    }
    stages {
        stage('Hello') {
            steps{
                echo 'Hello!!!'
                }
        }

        stage('Loging into Docker') {
            steps {
            sh "docker login -u ${docker_creds_USR} -p ${docker_creds_PSW}"
            }
        }

        stage('Building the Docker Image') {
            steps {
                script {
                    dockerImage = docker.build("asdpkp/nginx-webapp")
                    dockerImage.push("latest")
                }
            }
        }

        stage('Cleaning the cluster') {
            steps {
                echo 'here'
                    sh 'kubectl delete deployment nginx-hello-world'// -n nginx-app-namespace'
                    sh 'kubectl delete svc nginx-hello-worlds-svc'// -n nginx-app-namespace'
                    //sh 'kubectl delete namespace nginx-app-namespace'
                }
        }

        stage('Deploying the WebApp to the cluster') {
            steps{
                //sh 'kubectl create namespace nginx-app-namespace'
                sh 'kubectl apply -f webapp-deployment.yaml'// -n nginx-app-namespace
                }
        }
    }
}