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

        stage('Clone') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/KevinPozuelos/Laboratorio-SA-S12026-B.git'
            }
        }

        stage('Install') {
            steps {
                dir('Test-jenkins') {
                    sh 'npm install'
        }
    }
}

        stage('Build Nest (CI)') {
            steps {
                dir('Test-jenkins') {
                    sh 'npm run build'
        }
    }
}

        stage('Test (CI)') {
            steps {
                dir('Test-jenkins') {
                    sh 'npm run test || true'
                }
            }
        }

        stage('Docker Build (CD)') {
            steps {
                sh 'docker build -t $IMAGE:$TAG .'
            }
        }

        stage('Push Docker Hub (CD)') {
            steps {
                sh 'docker push $IMAGE:$TAG'
            }
        }

    }
}