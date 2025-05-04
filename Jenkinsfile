pipeline {
    agent any

    environment {
        DOCKER_HOST = 'tcp://host.docker.internal:2375'
    }

    stages {
        stage('Test Docker Access') {
            steps {
                sh 'docker version'
            }
        }

        stage('Install dependencies') {
            steps {
                dir('frontend') {
                    sh 'docker run --rm -v "${WORKSPACE}/frontend":/app -w /app node:18-alpine sh -c "npm install"'
                }
            }
        }

        stage('Build') {
            steps {
                dir('frontend') {
                    sh 'docker run --rm -v "${WORKSPACE}/frontend":/app -w /app node:18-alpine sh -c "npm run build"'
                }
            }
        }

        stage('Deploy to Firebase') {
            steps {
                dir('frontend') {
                    withCredentials([string(credentialsId: 'FIREBASE_TOKEN', variable: 'FIREBASE_TOKEN')]) {
                        sh '''
                            docker run --rm -v "${WORKSPACE}/frontend":/app -w /app node:18-alpine sh -c "
                              npm install -g firebase-tools && \
                              firebase deploy --token=$FIREBASE_TOKEN
                            "
                        '''
                    }
                }
            }
        }
    }
}
