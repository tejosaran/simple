pipeline {
    agent any

    stages {
        stage('Clone') {
            steps {
                echo 'Cloning repository...'
                git 'https://github.com/tejosaran/simple.git'
            }
        }

        stage('Build') {
            steps {
                echo 'Building application...'
                // You can add build commands here if needed
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying application...'
                // Copy files to web server directory (example for Ubuntu)
                sh 'sudo cp -r * /var/www/html/'
            }
        }
    }
}
