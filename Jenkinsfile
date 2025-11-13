pipeline {
    agent any

    environment {
        REPO_URL = "https://github.com/tejosaran/simple.git"
        DEPLOY_PATH = "/var/www/html"
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
                sh 'ls -l hello.html'
            }
        }

        stage('Test') {
            steps {
                echo "🧪 Testing project..."
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
                echo "🚀 Deploying project to ${DEPLOY_PATH}..."
                sh """
                cp hello.html ${DEPLOY_PATH}/hello.html
                chmod 644 ${DEPLOY_PATH}/hello.html
                echo "✅ hello.html deployed to ${DEPLOY_PATH} and Nginx reloaded"
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
