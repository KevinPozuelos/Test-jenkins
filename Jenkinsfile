pipeline {
    agent any

    tools {
        nodejs "node18"
    }

    environment {
        IMAGE = "kevinpozuelos/nest-app"
        TAG = "latest"
        QODANA_TOKEN = credentials('qodana-token')
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

        stage('Static Analysis (Qodana)') {
    agent {
        docker {
            image 'jetbrains/qodana-js'
            args "--entrypoint='' -v $WORKSPACE:/data/project"
        }
    }
    steps {
        sh 'qodana scan'
    }
}
        stage('Docker Build') {
            steps {
                sh 'docker build -t $IMAGE:$TAG .'
            }
        }

        stage('Push') {
    steps {
        withCredentials([usernamePassword(
            credentialsId: 'dockerhub',
            usernameVariable: 'DOCKER_USER',
            passwordVariable: 'DOCKER_PASS'
        )]) {
            sh '''
            echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin
            docker push $IMAGE:$TAG
            '''
        }
    }
}

    }
}