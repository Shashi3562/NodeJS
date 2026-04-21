pipeline {
    agent any

    environment {
        // This ensures Node.js is available in the Jenkins environment
        NODEJS_HOME = tool 'node' 
    }

    stages {
        stage('Checkout') {
            steps {
                // Pulls the latest code from your GitHub
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                // Installs the modules like Express, Mongoose, and Socket.io
                sh 'npm install'
            }
        }

        stage('Linter/Syntax Check') {
            steps {
                // A quick check to ensure there are no syntax errors in your JS files
                sh 'node --check server.js'
            }
        }

        stage('Run Automated Tests') {
            steps {
                // This triggers the test script defined in your package.json
                sh 'npm test'
            }
        }
    }
}
