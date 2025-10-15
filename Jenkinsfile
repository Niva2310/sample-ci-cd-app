pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh 'pip install -r requirements.txt'
            }
        }

        stage('Test') {
            steps {
                sh 'python -m unittest discover tests'
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


