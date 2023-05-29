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
                        apiVersion: apps/v1
                        kind: Deployment
                        metadata:
                        name: first-kube
                        labels:
                            app: first-kube
                        spec:
                        replicas: 2
                        selector:
                            matchLabels:
                            app: first-kube
                        template:
                            metadata:
                            labels:
                                app: first-kube
                            spec:
                            containers:
                            - name: first-kube
                                image: first-docker
                                imagePullPolicy: Never
                                resources:
                                limits:
                                    memory: "128Mi"
                                    cpu: "500m"
                                ports:
                                - containerPort: 8080
                    '''
                }
            }
            
            steps {
                script {
                    container('first_kube') {
                        sh 'ls -l'
                    }
                }
                
            }
        }
        
    }
}
