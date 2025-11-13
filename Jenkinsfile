// pipeline {
//     agent any

//     stages {
//         stage('Build') {
//             steps {
//                 echo '🔨 Building the Hello World project...'
//                 // Example: simulate build process
//                 sh 'echo "Hello World build successful!" > build.log'
//             }
//         }

//         stage('Test') {
//             steps {
//                 echo '🧪 Running tests...'
//                 // Example: check if build.log exists and contains text
//                 sh '''
//                 if [ -f build.log ] && grep -q "successful" build.log; then
//                     echo "✅ Test passed!"
//                 else
//                     echo "❌ Test failed!"
//                     exit 1
//                 fi
//                 '''
//             }
//         }
//     }

//     post {
//         success {
//             echo '🎉 Build and Test completed successfully!'
//         }
//         failure {
//             echo '❌ Build or Test failed. Check the logs above.'
//         }
//     }
// }

pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo '🔨 Building Hello World project...'
                // Create the Hello World HTML page
                sh 'echo "<h1>Hello World from Jenkins!</h1>" > build.log'
            }
        }

        stage('Test') {
            steps {
                echo '🧪 Running tests...'
                sh '''
                if [ -f build.log ] && grep -q "Hello World" build.log; then
                    echo "✅ Test passed!"
                else
                    echo "❌ Test failed!"
                    exit 1
                fi
                '''
            }
        }

        stage('Deploy') {
            steps {
                echo '🚀 Deploying to Nginx...'
                sh '''
                # Install Nginx if not installed
                if ! command -v nginx >/dev/null 2>&1; then
                    sudo apt update
                    sudo apt install -y nginx
                fi

                # Start and enable Nginx service
                sudo systemctl start nginx
                sudo systemctl enable nginx

                # Deploy the page
                sudo mv build.log /var/www/html/index.html

                # Optional: set proper permissions
                sudo chown www-data:www-data /var/www/html/index.html
                sudo chmod 644 /var/www/html/index.html

                echo "✅ Deployment completed!"
                '''
            }
        }
    }

    post {
        success {
            echo '🎉 Build, Test, and Deploy completed successfully!'
        }
        failure {
            echo '❌ Build/Test/Deploy failed. Check the logs above.'
        }
    }
}
