pipeline {
    agent any 
    environment {
        DOCKERHUB_CREDENTIALS = credentials('kapilgurjar')
    }
    stages { 
        stage('Build docker image') {
            steps {  
                node {
                    sh 'docker build -t vatsraj/pythonapp:$BUILD_NUMBER .'
                }
            }
        }
        stage('login to dockerhub') {
            steps {
                node {
                    withCredentials([usernamePassword(credentialsId: 'kapilgurjar', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                        sh "echo \$PASSWORD | docker login -u \$USERNAME --password-stdin"
                    }
                }
            }
        }
        stage('push image') {
            steps {
                node {
                    sh 'docker push vatsraj/pythonapp:$BUILD_NUMBER'
                }
            }
        }
    }
    post {
        always {
            node {
                sh 'docker logout'
            }
        }
    }
}
