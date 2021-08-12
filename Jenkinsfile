pipeline {
    agent any
    environment {
        dockerRun = "docker run -itd -p 80:80 --name wordpess ptemghare/wordpress"
    }
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
                sh 'docker login --username "ptemghare" --password "Sony@1902" docker.io'
                sh 'docker push ptemghare/wordpress:latest'
                sh 'docker push ptemghare/wordpress:1.0'
            }
        }
        stage('DockerDeploy') {
            steps {
                sshagent(['sshlogin-dev']) {
                    sh 'ssh -o StrictHostKeyChecking=no root@192.168.37.178 ${dockerRun}'
                }     
            }
        }
    }
}