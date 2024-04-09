pipeline {
    agent any 
    environment {
        DOCKERHUB_CREDENTIALS = credentials('kapilgurjar')
    }
    stages { 
        stage('Build docker image') {
            steps {  
                sh 'docker build -t vatsraj/pythonapp:$BUILD_NUMBER .'
            }
        }
        stage('login to dockerhub') {
            steps{
                withCredentials([usernamePassword(credentialsId: 'kapilgurjar', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                    sh "echo \$PASSWORD | docker login -u \$USERNAME --password-stdin"
                }
            }
        }
        stage('push image') {
            steps{
                sh 'docker push vatsraj/pythonapp:$BUILD_NUMBER'
            }
        }
    }
    post {
        always {
            sh 'docker logout'
        }
    }
}
