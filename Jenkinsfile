pipeline {
    agent any

    environment {
        FIREBASE_TOKEN = credentials('FIREBASE_TOKEN')
    }

    stages {
        stage('Install dependencies') {
            steps {
                script {
                    docker.image('node:18-alpine').inside('-u root') {
                        dir('frontend') {
                            sh 'npm install'
                        }
                    }
                }
            }
        }

        stage('Build') {
            steps {
                script {
                    docker.image('node:18-alpine').inside('-u root') {
                        dir('frontend') {
                            sh 'npm run build'
                        }
                    }
                }
            }
        }

        stage('Deploy to Firebase') {
            steps {
                script {
                    docker.image('node:18-alpine').inside('-u root') {
                        dir('frontend') {
                            sh 'npm install -g firebase-tools'
                            sh "firebase deploy --token $FIREBASE_TOKEN"
                        }
                    }
                }
            }
        }
    }
}