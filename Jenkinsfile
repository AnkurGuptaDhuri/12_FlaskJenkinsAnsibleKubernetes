pipeline {
    agent any

    stages {
        stage('checkout') {
            steps {
                echo 'Stage1: Checkout from GITHUB'
                checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/AnkurGuptaDhuri/python-docker-jenkins.git']])
            }
        }
        stage('Build Docker Image from Dockerfile') {
            steps {
                echo 'Stage2: Build docker Image'
                sh 'docker --version'
                echo 'Build number is ${BUILD_NUMBER}'
                sh 'docker build -t flaskapp:1.${BUILD_NUMBER} .'
            }
        }
         stage('Push Image to Docker Hub') {
            steps {
                echo 'Stage3: Image push to Docker Hub'
                withCredentials([gitUsernamePassword(credentialsId: 'docker_hub_tokenpwd', gitToolName: 'Default')]) {
                    sh 'docker push ankur5yk/12_flaskjenkinsansiblekubernetes:1.${BUILD_NUMBER}'
                }               
               /* sh 'docker tag flaskapp:1.${BUILD_NUMBER} ankur5yk/12_flaskjenkinsansiblekubernetes:1.${BUILD_NUMBER}'
                sh 'docker login -u ***** -p ****'*/
                
            }
        } 
    }
}
