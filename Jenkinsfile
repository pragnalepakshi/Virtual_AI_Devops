pipeline {
    agent any
    stages {
        stage('Pull Docker Image') {
            steps {
                sh 'docker pull urmsandeep/ai-artistic-style-service:latest'
            }
        }
        stage('Run Tests') {
            steps {
                sh 'docker run --rm -p 5001:5001 urmsandeep/ai-artistic-style-service pytest tests/'
            }
        }
        stage('Deploy Service') {
            steps {
                sh 'docker-compose down && docker-compose up -d'
            }
        }
        stage('Verify Deployment') {
            steps {
                sh 'curl -X POST http://127.0.0.1:5001/styleTransfer -F "image=@test.jpg" --output styled_output.jpg'
            }
        }
    }
    post {
        success {
            echo 'Pipeline executed successfully!'
        }
        failure {
            echo 'Pipeline failed. Check logs for errors.'
        }
    }
}
