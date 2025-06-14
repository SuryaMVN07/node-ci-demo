pipeline {
    agent any
    stages {
        stage('Clone GitHub Repo') {
            steps {
                git branch: 'main', url :'https://github.com/SuryaMVN07/node-ci-demo.git'
            }
        }
        stage('Install Dependencies') {
            steps {
                bat 'npm install'
            }
        }
        stage('Build Docker Image') {
            steps {
                bat 'docker build -t node-ci-demo .'
            }
        }
        stage('Run Docker Container') {
            steps {
                bat 'docker run -d -p 3000:3000 --name node-app node-ci-demo'
            }
        }
    }
    post {
        always {
            echo '✅ Build complete'
        }
    }
}
