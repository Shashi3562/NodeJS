pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/your-repo.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean compile'  // or gradle build, npm install
            }
        }

        stage('Unit Tests') {
            steps {
                sh 'mvn test'
                publishHTML target: [
                    reportDir: 'target/surefire-reports',
                    reportFiles: 'index.html',
                    reportName: 'Test Report'
                ]
            }
        }

        stage('Integration Tests') {
            steps {
                sh './scripts/integration-test.sh'
            }
        }

        stage('E2E Tests') {
            steps {
                sh 'npm run e2e'  // or selenium, cypress, etc.
            }
        }
    }

    post {
        always {
            junit 'target/surefire-reports/*.xml'  // Parse test results
            publishHTML target: [
                reportDir: 'test-results',
                reportFiles: 'index.html',
                reportName: 'Test Results'
            ]
        }
        failure {
            emailext(
                subject: "Build Failed: ${env.JOB_NAME}",
                body: "Tests failed. Check console output",
                to: "${env.CHANGE_AUTHOR_EMAIL}"
            )
        }
    }
}