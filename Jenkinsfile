pipeline {
    
    environment {
        dockerimagename = "first-docker"
        dockerImage = ""
        yamlFile = file('first_kube.yaml')
    }
    
    agent any

    stages {
        stage('Hello') {
            steps {
                echo 'Hello World'
                
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
                sshagent(['SSH-credentials']) {
                    sh 'ssh -o StrictHostKeyChecking=no -l albertchan host.docker.internal /usr/local/bin/docker build -t first-docker /Users/albertchan/Documents/Docker/First-docker'
                    sh 'ssh -o StrictHostKeyChecking=no -l albertchan host.docker.internal /usr/local/bin/kubectl delete deployment first-kube'
                }
            }
        }
        
        stage('Deploy to Kubernetes') {
            steps {
                sshagent(['SSH-credentials']) {
                    sh 'ssh -o StrictHostKeyChecking=no -l albertchan host.docker.internal /usr/local/bin/kubectl apply -f /Users/albertchan/Documents/Docker/First-docker/first_kube.yaml'
                }
            }
        }
        
    }
}
