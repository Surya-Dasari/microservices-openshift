pipeline {
    agent any

    stages {
        stage('Build & Tag Docker Image') {
            steps {
                sh "docker build -t suryadasari31/loadgenerator:latest ."
            }
        }
        
        stage('Push Docker Image') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'docker-cred',
                    usernameVariable: 'USER',
                    passwordVariable: 'PASS'
                )]) {
                    sh """
                    echo $PASS | docker login -u $USER --password-stdin
                    docker push suryadasari31/loadgenerator:latest
                    """
                }
            }
        }
    }
}
