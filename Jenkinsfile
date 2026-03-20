pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/an23304/NodeJS-app.git',
		credentialsId: 'github-pat'
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'sudo podman build -t node-app:latest .'
            }
        }
        stage('Deploy Container') {
            steps {
                sh '''
                sudo podman rm -f node-app || true
                sudo podman run -d --name node-app -p 3000:3000 node-app:latest
                '''
            }
        }
    }
}

