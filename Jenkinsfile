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
            }
        }
    }
}
