pipeline {
    agent any

    environment {
        DOCKERHUB_USERNAME = credentials('dockerhub-username')
        DOCKERHUB_PASSWORD = credentials('dockerhub-password')
        DOCKERHUB_IMAGE = 'jk1995/maven-app'
        DOCKERHUB_TAG = 'BUILD_NUMBER'
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