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

        stage('Build & Push Images') {
            parallel {

                stage('Order Service') {
                    steps {
                        dir('order-service') {
                            sh """
                              mvn clean package
                              docker build -t $REGISTRY/order-service:$TAG .
                              docker push $REGISTRY/order-service:$TAG
                            """
                        }
                    }
                }

                stage('User Service') {
                    steps {
                        dir('user-service') {
                            sh """
                              mvn clean package
                              docker build -t $REGISTRY/user-service:$TAG .
                              docker push $REGISTRY/user-service:$TAG
                            """
                        }
                    }
                }

                stage('Payment Service') {
                    steps {
                        dir('payment-service') {
                            sh """
                              mvn clean package
                              docker build -t $REGISTRY/payment-service:$TAG .
                              docker push $REGISTRY/payment-service:$TAG
                            """
                        }
                    }
                }

                stage('API Gateway') {
                    steps {
                        dir('api-gateway') {
                            sh """
                              mvn clean package
                              docker build -t $REGISTRY/api-gateway:$TAG .
                              docker push $REGISTRY/api-gateway:$TAG
                            """
                        }
                    }
                }
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sh """
                  kubectl set image deployment/order-service \
                    order-service=$REGISTRY/order-service:$TAG

                  kubectl set image deployment/user-service \
                    user-service=$REGISTRY/user-service:$TAG

                  kubectl set image deployment/payment-service \
                    payment-service=$REGISTRY/payment-service:$TAG

                  kubectl set image deployment/api-gateway \
                    api-gateway=$REGISTRY/api-gateway:$TAG
                """
            }
        }
    }
}
