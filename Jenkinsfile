pipeline {
    agent any

    stages {
        stage('GitCheckout') {
            steps {
                git(
                    branch: 'main',
                    credentialsId: 'github',
                    url: 'https://github.com/pravintemghare/wordpress.git'
                )    
            }
        }
        stage('DockerBuild') {
            steps {
                sh 'docker build -t ptemghare/wordpress:latest .'
            }
        }
        stage('DockerTag') {
            steps {
                sh 'docker tag ptemghare/wordpress:latest ptemghare/wordpress:latest'
                sh 'docker tag ptemghare/wordpress:latest ptemghare/wordpress:1.0'
            }
        }
        stage('DockerPush') {
            steps {
                withCredentials([string(credentialsId: 'dockerhubpwd', variable: 'dockerhubpwd')]) {
                sh 'docker login --username "ptemghare" --password ${dockerhubpwd} docker.io'
                }
                sh 'docker push ptemghare/wordpress:latest'
                sh 'docker push ptemghare/wordpress:1.0'
            }
        }
    }
}