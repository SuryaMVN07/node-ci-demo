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
                sh 'npm install'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh "docker build -t ${IMAGE_NAME} ."
            }
        }

        stage('Stop Existing Container (if any)') {
            steps {
                script {
                    // Stops and removes the container if it exists
                    sh "docker stop ${CONTAINER_NAME} || true"
                    sh "docker rm ${CONTAINER_NAME} || true"
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                sh "docker run -d -p ${PORT}:${PORT} --name ${CONTAINER_NAME} ${IMAGE_NAME}"
            }
        }
    }

    post {
        success {
            echo '✅ Build and deployment successful!'
        }
        failure {
            echo '❌ Build or deployment failed!'
        }
    }
}
