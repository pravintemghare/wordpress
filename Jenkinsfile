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
        stage('dockerbuild') {
            steps {
                sh 'docker build -t ptemghare/wordpress:latest .'
            }
        }
        stage('dockertag') {
            steps {
                sh 'docker tag ptemghare/wordpress:latest ptemghare/wordpress:latest'
                sh 'docker tag ptemghare/wordpress:latest ptemghare/wordpress:1.0'
            }
        }
        stage('dockerpush') {
            steps {
                sh 'docker login --username "ptemghare" --password "Sony@1902" docker.io'
                sh 'docker push ptemghare/wordpress:latest'
                sh 'docker push ptemghare/wordpress:1.0'
            }
        }
    }
}