pipeline {
    agent any

    environment {
        // Path where your web files should be deployed
        DEPLOY_PATH = "/var/www/html"
        // GitHub repo URL
        REPO_URL = "https://github.com/tejosaran/simple.git"
    }

    stages {
        stage('Checkout') {
            steps {
                echo "🔄 Pulling code from GitHub..."
                git url: "${REPO_URL}", branch: 'main'
            }
        }

        stage('Build') {
            steps {
                echo "🔨 Building project..."
                // For HTML, build could be just verifying files exist
                sh 'ls -l hello.html'
            }
        }

        stage('Test') {
            steps {
                echo "🧪 Testing project..."
                // Simple test: check if hello.html exists
                sh '''
                if [ ! -f hello.html ]; then
                    echo "ERROR: hello.html not found!"
                    exit 1
                else
                    echo "✅ hello.html exists"
                fi
                '''
            }
        }

        stage('Deploy') {
            steps {
                echo "🚀 Deploying project..."
                // Copy hello.html to deploy folder
                sh """
                cp hello.html ${DEPLOY_PATH}/hello.html
                echo "✅ Deployed to ${DEPLOY_PATH}"
                """
            }
        }
    }

    post {
        success {
            echo "🎉 Pipeline completed successfully!"
        }
        failure {
            echo "❌ Pipeline failed!"
        }
    }
}
