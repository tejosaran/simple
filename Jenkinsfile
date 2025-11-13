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

    environment {
        EC2_HOST = '18.223.106.64'   // Replace with your EC2 IP
        EC2_USER = 'ubuntu'
    }

    stages {
        stage('Build') {
            steps {
                echo '🔨 Building Hello World project...'
                sh 'echo "<h1>Hello World from Jenkins!</h1>" > hello.html'
            }
        }

        stage('Test') {
            steps {
                echo '🧪 Running tests...'
                sh 'test -f hello.html && echo "✅ File exists" || exit 1'
            }
        }

        stage('Deploy') {
            steps {
                echo '🚀 Deploying to EC2...'
                sshagent(['EC2_SSH_KEY']) {
                    sh '''
                    ssh -o StrictHostKeyChecking=no $EC2_USER@$EC2_HOST "mkdir -p /var/www/html"
                    scp -o StrictHostKeyChecking=no hello.html $EC2_USER@$EC2_HOST:/var/www/html/
                    '''
                }
            }
        }
    }

    post {
        success {
            echo '🎉 Build, Test, and Deploy completed successfully!'
        }
        failure {
            echo '❌ Build/Test/Deploy failed. Check logs.'
        }
    }
}

