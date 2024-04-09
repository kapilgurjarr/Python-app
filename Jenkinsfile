pipeline {
    agent any 
    environment {
        DOCKERHUB_CREDENTIALS = credentials('kapilgurjar')
    }
    stages { 
        stage('Build docker image') {
            steps {  
                node('any') {
                    sh 'docker build -t vatsraj/pythonapp:$BUILD_NUMBER .'
                }
            }
        }
        stage('login to dockerhub') {
            steps {
                node('any') {
                    withCredentials([usernamePassword(credentialsId: 'kapilgurjar', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                        sh "echo \$PASSWORD | docker login -u \$USERNAME --password-stdin"
                    }
                }
            }
        }
        stage('push image') {
            steps {
                node('any') {
                    sh 'docker push vatsraj/pythonapp:$BUILD_NUMBER'
                }
            }
        }
    }
    post {
        alway
