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
                docker run --network mongo-kakashka -e ME_CONFIG_MONGODB_SERVER=some-mongo -p 8081:8081 mongo-express
                '''
            }
        }
    }
}
