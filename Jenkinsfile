pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Knightfury786/hiring-app.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                 sh 'DOCKER_BUILDKIT=1 docker build -t hiring-app:latest .'
            }
        }

        stage('Push to DockerHub') {
            environment {
                DOCKERHUB_CREDENTIALS = credentials('docker')  // 'docker' is the credential ID
            }
            steps {
                sh """
                    echo \$DOCKERHUB_CREDENTIALS_PSW | docker login -u \$DOCKERHUB_CREDENTIALS_USR --password-stdin
                    docker tag hiring-app:latest sirajdevops/hiring-app:latest
                    docker push sirajdevops/hiring-app:latest
                """
            }
        }
    }
}
