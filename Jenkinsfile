pipeline {
    agent any
    
    tools{
        maven 'maven-new'
    }
    stages {
        stage('clone') {
            steps {
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/jai250/maven-web-app-ashokit.git']])
            }
        }
        stage('build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('docker image') {
            steps {
                sh 'docker build -t jk1995/maven-app:latest .'
            }
        }
        stage('k8s deployment') {
            steps {
                sh 'kubectl apply -f k8s-deploy.yml'   
    }
}        