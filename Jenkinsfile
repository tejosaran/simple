pipeline {
    agent any

    stages {
        stage('Clone') {
            steps {
                echo 'Repository already checked out by Jenkins SCM.'
            }
        }

        stage('Build') {
            steps {
                echo 'Building application...'
                // Example build steps if needed
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying application...'
                sh 'sudo cp -r * /var/www/html/'
            }
        }
    }
}
