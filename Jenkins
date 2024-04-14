pipeline {
    agent any
    
    tools {
        maven 'Maven'
    }
    
    stages {
        stage('Build Maven') {
            steps {
                checkout scmGit(
                    branches: [[name: '*/main']], 
                    extensions: [], 
                    userRemoteConfigs: [[url: 'https://github.com/AliZayan/Jenkins-Docker-Project']]
                )
                sh 'mvn clean install'
            }
        }
        
        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t alidevops/devops-integration .'
                }
            }
        }
        
        stage ('Push Image to Hub') {
            steps {
                script {
                    withCredentials([string(credentialsId: 'dockerhub-pwd', variable: 'dockerhubpwd')]) {
                        sh "docker login -u alizayan -p ${dockerhubpwd}"
                    }
                    sh 'docker push alizayan/devops-integration'
                }
            }
        }
        
        stage ('Deploy to Kubernetes') {
            steps {
                script {
                    kubernetesDeploy (configs: 'deploymentservice.yaml', kubeconfigId: 'ali')
                }
            }
        }
    }
}