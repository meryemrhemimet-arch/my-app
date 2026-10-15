pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/meryemrhemimet-arch/my-app.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build('meryem021/my-app')
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'dockerlogin') {
                        docker.image('meryem021/my-app').push('latest')
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                sh 'docker rm -f my-app || true'
                sh 'docker run -d --name my-app -p 3000:3000 meryem021/my-app:latest'
            }
        }
    }
}
