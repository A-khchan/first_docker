pipeline {
    
    environment {
        dockerimagename = "first-docker"
        dockerImage = ""
    }
    
    agent any

    stages {
        stage('Hello') {
            steps {
                echo 'Hello World'
                sh "whoami"
                sh "pwd"
                sh "ls -l /usr/bin/"
                sh "docker"
            }
        }
        
        stage('Checkout Source') {
            steps {
                git branch: 'main', url: 'https://github.com/A-khchan/first_docker.git'
            }
        }
        
        stage('Create docker image') {
            steps {
                script {
                    dockerImage = docker.build dockerimagename
                }
            }
        }
        
        stage('Deploy to Kubernetes') {
            steps {
                script {
                    kubernetesDeploy(configs: "first_kube.yaml", "first_service.yaml")
                }
            }
        }
        
    }
}
