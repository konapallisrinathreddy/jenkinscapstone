pipeline {
    agent any

    environment {
        DEPLOY_PORT = "82"
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                sh 'echo "Building the product..."'
                // Add build steps, like npm install, mvn clean package, etc.
            }
        }

        stage('Deploy') {
            when {
                branch 'master'
            }
            steps {
                sshPublisher(publishers: [sshPublisherDesc(configName: 'your-server', 
                    transfers: [sshTransfer(sourceFiles: '**', 
                        remoteDirectory: '/var/www/html', 
                        execCommand: "sudo systemctl restart nginx")])])
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully.'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}

