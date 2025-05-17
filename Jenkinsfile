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
        stage('Trivy Scan') {
            steps {
                sh 'trivy fs --format table -o fs.html .'
            }
        }
    }
}
