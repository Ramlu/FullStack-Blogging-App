pipeline {
    agent any 
    tools {
        jdk 'jdk17'
        maven 'maven3'
    }
    stages {
        stage('Clean Workspace') {
            steps {
                cleanWs()
            }
        }
        stage('java') {
            steps {
                echo "Started the pipeline"
                echo 'java --version'
            }
        }
        stage('Checkout') {
            steps {
                git branch: 'main', credentialsId: 'github-token', url: 'https://github.com/Ramlu/FullStack-Blogging-App.git'
            }
        }
        stage('Compile') {
            steps {
                sh 'mvn clean compile'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn install'
            }
        }
        stage('Package') {
            steps {
                sh 'mvn package'
            }
        }
    }
}
