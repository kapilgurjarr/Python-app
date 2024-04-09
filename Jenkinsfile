pipeline {
    agent any
    environment {
        DOCKERHUB_CREDENTIALS = credentials('kapilgurjar')
    }
    stages {
        stage('Build docker image') {
            steps {
                script {
                    docker.build("vatsraj/pythonapp:$BUILD_NUMBER")
                }
            }
        }
        stage('Login to DockerHub') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: 'kapilgurjar', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                        sh "echo $DOCKER_PASSWORD | docker login -u $DOCKER_USERNAME --password-stdin"
                    }
                }
            }
        }
        stage('Push image') {
            steps {
                script {
                    sh 'docker push vatsraj/pythonapp:$BUILD_NUMBER'
                }
            }
        }
    }
    post {
        always {
            script {
                sh 'docker logout'
            }
        }
    }
}
