cat > Jenkinsfile << 'EOF'
node {
    try {
        stage('Checkout') {
            echo "Checking out code from GitHub..."
            checkout scm
        }
        
        stage('Run Application') {
            echo "Running Node.js application..."
            sh 'node largest.js'
        }
        
    } catch (Exception e) {
        echo "Pipeline failed: ${e}"
        currentBuild.result = 'FAILURE'
    }
}
EOF
