pipeline {
    agent any

    tools {
        nodejs "node18"
    }

    environment {
        IMAGE = "kevinpozuelos/nest-app"
        TAG = "latest"
    }

    stages {

        stage('Install') {
            steps {
                sh 'npm install'
            }
        }

        stage('Build') {
            steps {
                sh 'npm run build'
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t $IMAGE:$TAG .'
            }
        }

        stage('Push') {
            steps {
                sh 'docker push $IMAGE:$TAG'
            }
        }

    }
}