pipeline {
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
stage('Test') {
            steps {
                sh './mvnw test'
            }
        }

        stage('Push to Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-credentials', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                    sh 'echo $DOCKER_PASSWORD | docker login -u $DOCKER_USERNAME --password-stdin'
                    sh 'docker tag order_service:latest your_dockerhub_username/order_service:latest'
                    sh 'docker push your_dockerhub_username/order_service:latest'
                }
            }
        }
    }

    post {
        always {
            cleanWs()
        }
    }
}