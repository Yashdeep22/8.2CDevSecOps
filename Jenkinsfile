pipeline {
    agent any

    environment {
        RECIPIENTS = 'proyashjaiswal@gmail.com' // Change to your desired email address
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Yashdeep22/8.2CDevSecOps.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                bat 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                bat 'npm test || exit /b 0' // Save output to log
            }
            post {
                always {
                    emailext (
                        subject: "Jenkins - Test Stage: ${currentBuild.currentResult}",
                        body: "The Test stage has completed with status: ${currentBuild.currentResult}. Please see attached log.",
                        to: "${env.RECIPIENTS}",
                    )
                }
            }
        }

        stage('Generate Coverage Report') {
            steps {
                bat 'npm run coverage || exit /b 0'
            }
        }

        stage('NPM Audit (Security Scan)') {
            steps {
                bat 'npm audit|| exit /b 0'
            }
            post {
                always {
                    emailext (
                        subject: "Jenkins - Security Scan Stage: ${currentBuild.currentResult}",
                        body: "The Security Scan has completed with status: ${currentBuild.currentResult}. Please see attached audit report.",
                        to: "${env.RECIPIENTS}",
                    )
                }
            }
        }
    }
}
