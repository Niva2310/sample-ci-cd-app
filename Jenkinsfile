pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                bat 'python -m venv venv'
                bat 'venv\\Scripts\\activate && pip install -r requirements.txt'
            }
        }

        stage('Test') {
            steps {
                bat 'venv\\Scripts\\activate && python -m unittest discover tests'
            }
        }

        stage('Deploy') {
            steps {
                echo "Deployment step - configure to deploy to AWS EC2 or Elastic Beanstalk"
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
