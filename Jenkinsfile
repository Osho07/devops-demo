pipeline {
    agent any
    environment {
        DOCKER_CREDENTIALS = credentials('docker-hub-credentials')
        IMAGE_NAME = "osho07/devops-demo"
    }
    stages {
        stage('Checkout Code') {
            steps {
                git 'https://github.com/Osho07/devops-demo.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t $IMAGE_NAME .'
                }
            }
        }
        stage('Push to Docker Hub') {
            steps {
                script {
                    sh '''
                    echo $DOCKER_CREDENTIALS_PSW | docker login -u $DOCKER_CREDENTIALS_USR --password-stdin
                    docker push $IMAGE_NAME
                    '''
                }
            }
        }
        stage('Cleanup') {
            steps {
                sh 'docker rmi $IMAGE_NAME'
            }
        }
    }
}
