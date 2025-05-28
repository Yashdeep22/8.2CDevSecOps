pipeline {
    agent any


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
                        subject: "Jenkins - Test Stage: ",
                        body: "The Test stage has completed with status.",
                        to: "yashdeepsinghvilkhu@gmail.com",
                    )
                }
            }
        }
// ${currentBuild.currentResult}  ${currentBuild.currentResult}  ${env.RECIPIENTS}
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
                        subject: "Jenkins - Security Scan Stage: ",
                        body: "The Scan stage has completed with status.",
                        to: "yashdeepsinghvilkhu@gmail.com",
                    )
                }
            }
        }
    }
}
