pipeline {
    agent any
    tools {
        maven 'maven-3.9.7'
    }
    stages {
        stage ('Build Maven'){
            steps{
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/rajivsiddiqui/jenkins-java-maven']])
                sh 'mvn clean install'
            }
        }
        stage ('Build Docker image'){
            steps{
                script{
                    sh 'docker build -t rajivsiddiqui/devops-integration .'
                }
            }
        }
        stage ('push docker image'){
            steps{
                script{
                    withCredentials([string(credentialsId: 'docker-hub-password', variable: 'dockerhubpassword')]) {
                    sh 'docker login -u rajivsiddiqui -p ${dockerhubpassword}'
                    }
                    sh 'docker push rajivsiddiqui/devops-integration'
                } 
            }
        }
    }
    
}