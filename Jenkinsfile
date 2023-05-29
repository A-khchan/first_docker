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
                script {
                    def yamlFile = file('first_kube.yaml')
                    kubernetes {
                        yaml yamlFile
                    }
                }
            }
            
            steps {
                script {
                    //kubernetesApply(file: "first_kube.yaml", environment: "dev")
                    //kubernetesApply(file: "first_service.yaml", environment: "dev")
                    def yamlFile = file('first_kube.yaml')
                    kubernetes {
                        yaml yamlFile
                    }
                }
                
            }
        }
        
    }
}
