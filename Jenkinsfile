pipeline {
    agent any

    environment {
        REGISTRY = "rajeevreddy1511"
        TAG = "${BUILD_NUMBER}"
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Order Service') {
            steps {
                dir('order-service') {
                    sh 'mvn clean package'
                    sh 'docker build -t $REGISTRY/order-service:$TAG .'
                    sh 'docker push $REGISTRY/order-service:$TAG'
                }
            }
        }

        stage('Build User Service') {
            steps {
                dir('user-service') {
                    sh 'mvn clean package'
                    sh 'docker build -t $REGISTRY/user-service:$TAG .'
                    sh 'docker push $REGISTRY/user-service:$TAG'
                }
            }
        }

        stage('Build Payment Service') {
            steps {
                dir('payment-service') {
                    sh 'mvn clean package'
                    sh 'docker build -t $REGISTRY/payment-service:$TAG .'
                    sh 'docker push $REGISTRY/payment-service:$TAG'
                }
            }
        }

        stage('Build API Gateway') {
            steps {
                dir('api-gateway') {
                    sh 'mvn clean package'
                    sh 'docker build -t $REGISTRY/api-gateway:$TAG .'
                    sh 'docker push $REGISTRY/api-gateway:$TAG'
                }
            }
        }
    }
}
