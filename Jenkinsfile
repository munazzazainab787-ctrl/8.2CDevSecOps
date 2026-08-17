pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/munazzazainab787-ctrl/8.2CDevSecOps.git'
            }
        }
        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }
        stage('Run Tests') {
            steps {
                sh 'npm test || true'
            }
            post {
                always {
                    emailext(
                        subject: "Test Stage: ${currentBuild.currentResult} - Build #${env.BUILD_NUMBER}",
                        body: "The Run Tests stage completed with status: ${currentBuild.currentResult}. See attached log.",
                        to: "munazzazainab787@gmail.com",
                        attachLog: true
                    )
                }
            }
        }
        stage('Generate Coverage Report') {
            steps {
                sh 'npm run coverage || true'
            }
        }
        stage('NPM Audit (Security Scan)') {
            steps {
                sh 'npm audit || true'
            }
            post {
                always {
                    emailext(
                        subject: "Security Scan Stage: ${currentBuild.currentResult} - Build #${env.BUILD_NUMBER}",
                        body: "The NPM Audit (Security Scan) stage completed with status: ${currentBuild.currentResult}. See attached log.",
                        to: "munazzazainab787@gmail.com",
                        attachLog: true
                    )
                }
            }
        }
    }
}
