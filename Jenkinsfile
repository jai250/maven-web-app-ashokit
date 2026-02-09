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
    }
}        