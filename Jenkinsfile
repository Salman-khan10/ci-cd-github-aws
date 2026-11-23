pipeline {
    agent any

    environment {
        CONTAINER_NAME = 'nestjs-app'
        IMAGE_NAME = 'nestjs-image'
        EMAIL = "karansmishra.84@gmail.com "
        PORT = "3000"
        
    }

    stages {
        stage('clone repo') {
            steps {
                git branch: 'main', url: 'https://github.com/Salman-khan10/ci-cd-github-aws'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t $IMAGE_NAME .'
                }
            }
        }
        stage('stop and remove container') {
            steps {
                script {
                    sh 'docker stop $CONTAINER_NAME || true'
                    sh 'docker rm $CONTAINER_NAME || true'
                }
            }
        }
        stage('Run Docker Container') {
            steps {
                script {
                    sh '''
                    docker run -d -p $PORT:$PORT --name $CONTAINER_NAME $IMAGE_NAME
                    '''
                }
            }
        }
        stage('Send Email Notification') {
            steps {
                script {
                    emailext (
                        subject: "Jenkins Build Notification",
                        body: "The Jenkins build has completed successfully.!n\nYou can access the application at: http://51.20.137.63:3000/",
                        to: "$EMAIL"
                    )
                }
            }
        }
    }
}