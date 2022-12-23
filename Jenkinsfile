pipeline {
    agent any

    environment {
        registry = "25A9D16E3804BE622D5E32FE3B8B1175.yl4.ca-central-1.eks.amazonaws.com"
    }
    
    stages {
        stage('Checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/pankajghansela/SpringbootApp_EKS-Docker-Jenkins.git']]])
            }
        }
    
        stage ("Build image") {
            steps {
                script {
                    docker.build registry
                }
            }
        }
        
        stage ("docker push") {
         steps {
             script {
                sh "aws ecr get-login-password --region ca-central-1 | docker login --username AWS --password-stdin 25A9D16E3804BE622D5E32FE3B8B1175.yl4.ca-central-1.eks.amazonaws.com"
                sh "docker push 25A9D16E3804BE622D5E32FE3B8B1175.yl4.ca-central-1.eks.amazonaws.com/Demo_EKSrepo"
                 
             }
           }   
        }
        
        stage ("Kube Deploy") {
            steps {
                withKubeConfig(caCertificate: '', clusterName: '', contextName: '', credentialsId: 'K8S', namespace: '', serverUrl: '') {
                 sh "kubectl apply -f eks-deployment.yaml"
                }
            }
        }
    }
}
