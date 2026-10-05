pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/TM-manoj/devops-project1.git'
            }
        }

        stage('Build and Test') {
            steps {
                sh 'mvn clean test'
                sh 'mvn package -DskipTests'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t devops-project1:1.0 .'
            }
        }

        stage('Push Docker Image') {
            steps {
                withCredentials([
                    usernamePassword(
                        credentialsId: '4ca14fe7-1b25-4b65-9ecb-b4370e341fff',
                        usernameVariable: 'DOCKER_USERNAME',
                        passwordVariable: 'DOCKER_PASSWORD'
                    )
                ]) {
                    sh '''
                        echo "$DOCKER_PASSWORD" | docker login -u "$DOCKER_USERNAME" --password-stdin
                        docker tag devops-project1:1.0 "$DOCKER_USERNAME/devops-project1:1.0"
                        docker push "$DOCKER_USERNAME/devops-project1:1.0"
                        docker logout
                    '''
                }
            }
        }
    }
}
