pipeline {
    agent any
    
    stages {
        stage('create docker image mongodb') {
            steps {
                sh '''
                docker build -t chikibevchik/mongo:mongodb .
                docker push chikibevchik/mongo:mongodb
                '''
            }
        }
        stage('create docker image mongo express') {
            steps {
                git 'https://github.com/skalajonson/mongo-express.git'
                withCredentials([usernamePassword(credentialsId: 'DockerHub-Credentials', usernameVariable: 'skalajonson', passwordVariable: 'q59p8w8c')]) {
                sh '''
                docker build -t chikibevchik/mongo:mongo-express .
                docker push chikibevchik/mongo:mongo-express
                '''
                }
            }
        }
        stage('Create docker network') {
            steps {
                sh '''
                docker network create mongo-kakashka
                '''
            }
        }
        stage('run mongo database') {
            steps {
                sh '''
                docker run -d --name mongo-container --network mongo-kakashka -p 27017:27017 mongo

                '''
            }
        }
        stage('run mongo express') {
            steps {
                sh '''
                docker run -d --name mongo-express-container --network mongo-kakashka -p 8081:8081 -e ME_CONFIG_MONGODB_SERVER=mongo-container -e ME_CONFIG_BASICAUTH_USERNAME=admin -e ME_CONFIG_BASICAUTH_PASSWORD=password mongo-express

                '''
            }
        }
    }
}
