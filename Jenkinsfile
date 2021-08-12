pipeline {
    agent_any
    stages {
        stage('GitCheckout') {
            step {
                git branch: 'main'
                    credentailsId: 'github'
                    url: 'https://github.com/pravintemghare/wordpress.git'
            }
        }
        stage('dockerbuild') {
            step {
                sh 'docker build -t prtemgha/wordpress:latest .'
            }
        }
        stage('dockertag') {
            step {
                sh 'docker tag prtemgha/wordpress:latest prtemgha/wordpress:latest'
                sh 'docker tag prtemgha/wordpress:latest prtemgha/wordpress:1.0'
            }
        }
        stage('dockerpush') {
            step {
                sh 'docker login --username "ptemghare" --password "Sony@1902" docker.io'
                sh 'docker push prtemgha/wordpress:latest'
                sh 'docker push prtemgha/wordpress:1.0'
            }
        }
    }
}