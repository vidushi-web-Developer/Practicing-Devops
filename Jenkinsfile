pipeline {
    agent any

    environment {
        IMAGE_NAME = "my-html-app"
        CONTAINER_NAME = "html-container"
        PORT = "3000"
    }

    stages {

        stage('Clone Repo') {
            steps {
                git branch: 'main', url: 'https://github.com/your-username/your-repo.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Stop Old Container') {
            steps {
                sh '''
                docker stop $CONTAINER_NAME || true
                docker rm $CONTAINER_NAME || true
                '''
            }
        }

        stage('Run New Container') {
            steps {
                sh '''
                docker run -d -p $PORT:80 --name $CONTAINER_NAME $IMAGE_NAME
                '''
            }
        }
    }

    post {
        success {
            mail to: 'your-email@gmail.com',
                 subject: "✅ Build Success",
                 body: "Your app deployed successfully!"
        }

        failure {
            mail to: 'your-email@gmail.com',
                 subject: "❌ Build Failed",
                 body: "Check Jenkins logs."
        }
    }
}
