pipeline {
    agent any

    environment {
        IMAGE_NAME = "sync-service"
    }

    stages {

        stage('Checkout') {
            steps {
                git 'https://github.com/sai-98-demo/cloudeagle-devops-assignment.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Deploy to QA') {
            when {
                branch 'develop'
            }
            steps {
                echo "Deploying to QA environment"
            }
        }

        stage('Deploy to Staging') {
            when {
                branch 'staging'
            }
            steps {
                echo "Deploying to Staging environment"
            }
        }

        stage('Deploy to Production') {
            when {
                branch 'main'
            }
            steps {
                input "Approve production deployment?"
                echo "Deploying to Production"
            }
        }
    }
}
