pipeline {
    agent any

    tools {
        
        nodejs 'node'
    }

    environment {
        
        MONGO_URI = 'mongodb://localhost:27017/myapp'
    }

    stages {
        stage('Checkout') {
            steps {
                // Git se code pull kia jenkins ny automatic
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                echo 'Installing node modules...'
                sh 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                echo 'Running tests...'
                
                sh 'npm test || echo "No tests specified"'
            }
        }

        stage('Deploy Application') {
            steps {
                echo 'Deploying Application...'
                // Yahan app ko restart 
                sh 'pm2 restart my-node-app || pm2 start server.js --name "my-node-app"'
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Check logs!'
        }
    }
}
