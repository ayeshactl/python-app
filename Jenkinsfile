pipeline {
    agent any

    environment {
        VENV = "venv"
    }

    stages {

        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Setup Virtual Environment') {
            steps {
                sh '''
                python3 -m venv venv
                . venv/bin/activate
                pip install --upgrade pip
                pip install -r requirements.txt
                '''
            }
        }

        stage('Run Tests') {
            steps {
                sh '''
                . venv/bin/activate
                pytest -v
                '''
            }
        }
    }

    post {
        always {
            echo "Pipeline finished"
        }

        success {
            echo "✅ Build + Tests Passed"
        }

        failure {
            echo "❌ Build Failed - check logs"
        }
    }
}
