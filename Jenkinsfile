pipeline {
    agent any

    environment {
        VENV_DIR = "venv"
        AWS_EC2_USER = "ec2-user"              // your EC2 username
        AWS_EC2_HOST = "your-ec2-ip"           // your EC2 public IP
        AWS_EC2_KEY = "C:\\path\\to\\your\\key.pem" // path to private key
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Niva2310/sample-ci-cd-app.git'
            }
        }

        stage('Build') {
            steps {
                bat "python -m venv %VENV_DIR%"
                bat "%VENV_DIR%\\Scripts\\activate && pip install -r requirements.txt"
            }
        }

        stage('Test') {
            steps {
                bat "%VENV_DIR%\\Scripts\\activate && python -m unittest discover tests"
            }
        }

        stage('Deploy') {
            steps {
                echo "Deploying Flask app to AWS EC2..."
                // Copy files using native scp
                bat """
                scp -i %AWS_EC2_KEY% -r * %AWS_EC2_USER%@%AWS_EC2_HOST%:/home/%AWS_EC2_USER%/app/
                """
                // SSH and start app in background
                bat """
                ssh -i %AWS_EC2_KEY% %AWS_EC2_USER%@%AWS_EC2_HOST% "cd /home/%AWS_EC2_USER%/app && python3 -m venv venv && source venv/bin/activate && pip install -r requirements.txt && nohup python3 app.py &"
                """
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed! Check console output for details.'
        }
    }
}
