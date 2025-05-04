pipeline {
    agent any

    stages {
        stage('Install dependencies') {
            agent {
                docker {
                    image 'node:18-alpine'
                    args '-v $PWD/frontend:/app -w /app'
                }
            }
            steps {
                sh 'npm install'
            }
        }

        stage('Build') {
            agent {
                docker {
                    image 'node:18-alpine'
                    args '-v $PWD/frontend:/app -w /app'
                }
            }
            steps {
                sh 'npm run build'
            }
        }

        stage('Deploy to Firebase') {
            agent {
                docker {
                    image 'node:18-alpine'
                    args '-v $PWD/frontend:/app -w /app'
                }
            }
            steps {
                withCredentials([string(credentialsId: 'FIREBASE_TOKEN', variable: 'FIREBASE_TOKEN')]) {
                    sh 'npm install -g firebase-tools'
                    sh 'firebase deploy --token "$FIREBASE_TOKEN"'
                }
            }
        }
    }
}