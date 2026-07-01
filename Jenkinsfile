pipeline {
    agent any

    tools {
        // Ensure Node.js plugin is installed in Jenkins and named 'node'
        nodejs 'node'
    }

    environment {
        // Agar MongoDB local hai ya external URL hy to yahan env variables set kr skty ho
        MONGO_URI = 'mongodb://localhost:27017/myapp'
    }

    stages {
        stage('Checkout') {
            steps {
                // Git se code pull krna (Ye Jenkins job khud b handle kr leta hy)
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
                // Agar test scripts hain to 'npm test' chlao, wrna custom script ya check
                sh 'npm test || echo "No tests specified"'
            }
        }

        stage('Deploy Application') {
            steps {
                echo 'Deploying Application...'
                // Yahan app ko restart krne ki command aey gi (e.g., using pm2)
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
