pipeline {
    agent any
    
    stages {
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
                docker run -p 27017:21017 -d -e MONGO_INITDB_ROOT_USERNAME=admin -e MONGO_INITDB_ROOT_PASSWORD=password --name mongodb --net mongo-kakashka mongo
                '''
            }
        }
        stage('run mongo express') {
            steps {
                sh '''
                docker run -d -p 8081:8081 -e ME_CONFIG_MONGODB_ADMINUSER=admin -e ME_CONFIG_MONGODB_ADMINPASSWORD=password --name mongo_express --net mongo-kakashka -e ME_CONFIG_MONGODB_SERVER=mongodb mongo-express:0.54.0
                '''
            }
        }
    }
}
