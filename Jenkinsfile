pipeline {
    agent any

    environment {
        DOCKERHUB_IMAGE = 'jk1995/maven-app'
        DOCKERHUB_TAG = "${BUILD_NUMBER}"
    }
    
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
        stage('docker-build') {
            steps {
                sh 'docker build -t $DOCKERHUB_IMAGE:$DOCKERHUB_TAG .'
            }
        }
        stage('docker-push') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker-token', passwordVariable: 'docker_password', usernameVariable: 'docker_user')]) {
                    sh 'echo $docker_password | docker login -u $docker_user --password-stdin'
                    sh 'docker push $DOCKERHUB_IMAGE:$DOCKERHUB_TAG'
                }
               
            }
        
        }
        stage('deploy to kubernetes') {
            steps {
                sh 'kubectl apply -f k8s-deploy.yml'
            }
        }     
    }
}    
                