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
        sh 'echo "Hello World build successful!" > build.log'
    }
}


        stage('Test') {
            steps {
                echo '🧪 Running tests...'
                sh '''
                if [ -f build.log ] && grep -q "successful" build.log; then
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
                echo '🚀 Deploying to /var/www/html/...'
                sh 'sudo cp build.log /var/www/html/build.log'
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
