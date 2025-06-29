pipeline {Add commentMore actions
    agent any

    stages {
        stage('Clone') {
            steps {
                git branch: 'main', url: 'https://github.com/0xbakry/order_service.git'

            }
        }

        stage('Build') {
            steps {
                sh './mvnw clean package -DskipTests'
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t order_service:latest .'
            }
        }

        stage('Docker Run') {
            steps {
                sh 'docker run -d -p 8080:8080 --name order_service order_service:latest'
            }
        }
    }
}