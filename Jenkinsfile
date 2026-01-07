pipeline {
    agent any

    stages {

        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Build Order Service') {
            steps {
                dir('order-service') {
                    sh 'mvn clean package'
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                dir('order-service') {
                    sh 'docker build -t order-service:ci .'
                }
            }
        }
    }
}
