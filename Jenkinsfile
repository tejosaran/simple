pipeline {
    agent any

    environment {
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

        stage('Setup Nginx') {
            steps {
                echo "⚙️ Ensuring Nginx is installed..."
                sh '''
                if ! command -v nginx >/dev/null 2>&1; then
                    echo "Nginx not found. Installing..."
                    # Ubuntu/Debian
                    if [ -f /etc/debian_version ]; then
                        sudo apt update
                        sudo apt install nginx -y
                        sudo systemctl enable nginx
                        sudo systemctl start nginx
                    # CentOS/RHEL
                    elif [ -f /etc/redhat-release ]; then
                        sudo yum install epel-release -y
                        sudo yum install nginx -y
                        sudo systemctl enable nginx
                        sudo systemctl start nginx
                    fi
                else
                    echo "Nginx is already installed."
                    sudo systemctl start nginx || true
                fi
                '''
            }
        }

        stage('Deploy') {
            steps {
                echo "🚀 Deploying project..."
                sh '''
                # Detect Nginx root automatically
                ROOT=$(nginx -T 2>/dev/null | grep -oP 'root\s+\K[^;]+' | head -1)
                echo "Detected Nginx root: $ROOT"

                # Copy hello.html
                sudo cp hello.html $ROOT/hello.html
                sudo chown $(whoami):$(whoami) $ROOT/hello.html
                sudo chmod 644 $ROOT/hello.html

                # Reload Nginx
                sudo systemctl reload nginx
                echo "✅ hello.html deployed to $ROOT and Nginx reloaded"
                '''
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
