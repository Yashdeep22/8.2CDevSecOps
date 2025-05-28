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
                bat 'npm test || exit /b 0'
            }
            post {
                always {
                    emailext (
                        subject: "Jenkins - Test Stage",
                        body: """The Test stage has completed.Check the attached log for more details.""",
                        to: "yashdeepsinghvilkhu@gmail.com",
                        attachLog: true,
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
                bat 'npm audit || exit /b 0'
            }
            post {
                always {
                    emailext (
                        subject: "Jenkins - Security Scan Stage",
                        body: """The Security Scan stage has completed. Check the attached log for more details.""",
                        to: "yashdeepsinghvilkhu@gmail.com",
                        attachLog: true,
                    )
                }
            }
        }
    }
}
