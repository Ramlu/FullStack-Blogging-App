pipeline {
    agent any 
    tools {
        jdk 'jdk17'
        maven 'maven3'
    }
    environment {
        SCANNER_HOME = tool 'sonar-scanner'
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
        stage('Trivy Scan') {
            steps {
                sh 'trivy fs --format table -o fs.html .'
            }
        }
        stage('Sonar anaylysis') {
            steps {
                withSonarQubeEnv('sonar-server') {
                sh '''
                    $SCANNER_HOME/bin/sonar-scanner \
                    -Dsonar.projectName="Blogging-app" \
                    -Dsonar.projectKey="Blogging-app" \
                    -Dsonar.java.binaries="target"
            '''
                }
            }
        }
        stage('Package') {
            steps {
                sh 'mvn package'
            }
        }
        stage('Deploy') {
            steps {
                withMaven(globalMavenSettingsConfig: '33b45880-0672-4bc6-9e98-2ef2d276275f', jdk: 'jdk17', maven: 'maven3', mavenSettingsConfig: '', traceability: true) {
                sh 'mvn deploy'
                }
            }
        }
    }
}
