pipeline {

    agent any

    environment {
        IMAGE_NAME = "eureka-server"
    }

    stages {

        stage('Checkout') {
            steps {
               checkout scm
            }
        }

        stage('Build JAR') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Run Container') {
            steps {
                sh '''
                docker stop eureka-server || true
                docker rm eureka-server || true

                docker run -d \
                  --name eureka-server \
                  -p 8761:8761 \
                  $IMAGE_NAME
                '''
            }
        }
    }
}