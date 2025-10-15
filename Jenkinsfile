pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/Niva2310/sample-ci-cd-app.git'
            }
        }

        stage('Set up Python Environment') {
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
                    python -m unittest discover tests
                '''
            }
        }

        stage('Deploy') {
            steps {
                echo "🚀 Deployment step - configure to deploy to AWS EC2 or Elastic Beanstalk"
            }
        }
    }

    post {
        success {
            echo '✅ Pipeline completed successfully!'
        }
        failure {
            echo '❌ Pipeline failed! Check console output for details.'
        }
    }
}
