pipeline {
    agent any

    stages {
        stage('Fetch from git') {
            steps {
                git branch: 'main', url: 'https://github.com/Kishanrampure/Jenkins_basic.git'
            }
        }
        stage('Build image') {
            steps {
                sh 'docker build -t kishanrampure/notes:v${BUILD_TIMESTAMP} .'
            }
        }
       stage('Push to dockerhub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-credentials', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                sh 'docker login -u $USERNAME -p $PASSWORD' 
                sh 'docker push kishanrampure/notes:v${BUILD_TIMESTAMP}'
               }
            }
        }   
       stage('Docker Run') {
             steps {
                sh 'docker-compose down && docker-compose up -d'
            }
        }
    }
}

