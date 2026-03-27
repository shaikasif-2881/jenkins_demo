pipeline {
    agent any

    environment {
        DOCKER_HUB = "asifuserdocker"
    }

    stages {

        stage('Clone') {
            steps {
                git branch: 'main', url: 'https://github.com/shaikasif-2881/jenkins_demo.git'
            }
        }

        stage('Build Backend Image') {
            steps {
                sh 'docker build -t $DOCKER_HUB/backend ./backend'
            }
        }

        stage('Build Frontend Image') {
            steps {
                sh 'docker build -t $DOCKER_HUB/frontend ./frontend'
            }
        }

        stage('Push Images') {
            steps {
                sh 'docker push $DOCKER_HUB/backend'
                sh 'docker push $DOCKER_HUB/frontend'
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                docker stop app || true
                docker rm app || true
                docker run -d -p 80:80 $DOCKER_HUB/frontend
                '''
            }
        }
    }
}