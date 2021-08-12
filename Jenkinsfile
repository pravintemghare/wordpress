pipeline {
    agent any

    stages {
        stage('GitCheckout') {
            steps {
                git branch: 'main'
                    credentailsId: 'github'
                    url: 'https://github.com/pravintemghare/wordpress.git'
            }
        }
        stage('dockerbuild') {
            steps {
                sh 'docker build -t prtemgha/wordpress:latest .'
            }
        }
        stage('dockertag') {
            steps {
                sh 'docker tag prtemgha/wordpress:latest prtemgha/wordpress:latest'
                sh 'docker tag prtemgha/wordpress:latest prtemgha/wordpress:1.0'
            }
        }
        stage('dockerpush') {
            steps {
                sh 'docker login --username "ptemghare" --password "Sony@1902" docker.io'
                sh 'docker push prtemgha/wordpress:latest'
                sh 'docker push prtemgha/wordpress:1.0'
            }
        }
    }
}