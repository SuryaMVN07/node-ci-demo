pipeline {
    agent any

    environment {
        IMAGE_NAME = 'node-ci-demo'
        CONTAINER_NAME = 'node-app'
        PORT = '3000'
    }

    stages {
        stage('Clone GitHub Repo') {
            steps {
                git branch: 'main', url: 'https://github.com/SuryaMVN07/node-ci-demo.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                bat 'npm install'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat "docker build -t %IMAGE_NAME% ."
            }
        }

        stage('Stop Existing Container (if any)') {
            steps {
                bat "docker stop %CONTAINER_NAME% || exit 0"
                bat "docker rm %CONTAINER_NAME% || exit 0"
            }
        }

        stage('Run Docker Container') {
            steps {
                bat "docker run -d -p %PORT%:3000 --name %CONTAINER_NAME% %IMAGE_NAME%"
            }
        }
    }

    post {
        success {
            echo '✅ Application deployed successfully!'
        }
        failure {
            echo '❌ Build or deployment failed!'
        }
    }
}
