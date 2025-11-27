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
                sh '/usr/bin/trivy fs --format table --output trivy-fs-report.html .'
            }
        }
        stage('SonarQube Analsyis') {
            steps {
                withSonarQubeEnv('sonar') {
                    sh ''' sonar-scanner -Dsonar.projectName=BoardGame -Dsonar.projectKey=BoardGame \
                            Dsonar.sources=. -Dsonar.java.binaries=target/classes -Dsonar.exclusions=**/trivy-image-report.html'''
                }
            }
        }
    }
}
