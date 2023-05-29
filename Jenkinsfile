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
            }
        }
        
        stage('Deploy to Kubernetes') {
            agent {
                kubernetes {
                    yaml '''
                        apiVersion: v1
                        kind: Pod
                        spec:
                            containers:
                            - name: agentpod
                              image: first-docker
                              ports:
                              - containerPort: 8080
                    '''
                }
            }
            
            steps {
                script {
                    container('agentpod') {
                        sh 'ls -l'
                    }
                }
                
            }
        }
        
    }
}
