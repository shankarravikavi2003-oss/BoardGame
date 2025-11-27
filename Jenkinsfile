pipeline {
    agent any
    tools {
        maven 'maven3'
    }
    stages {
        stage('Git Checkout') {
            steps {
                git 'https://github.com/shankarravikavi2003-oss/BoardGame.git'
            }
        }
        stage('Compile') {
            steps {
                sh 'mvn compile'
                echo 'GITHUB Webhook Configured'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
        stage('File System Scan') {
            steps {
                sh 'trivy fs --format table --output trivy-fs-report.html .'
            }
        }
    }
}
