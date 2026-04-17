pipeline {
    agent any

    stages {

        stage('Build Image') {
            steps {
                sh 'docker build -t kavyasekar00/myapp:latest .'
            }
        }

        stage('Push Image') {
            steps {
                withDockerRegistry([credentialsId: 'docker-hub-creds', url: '']) {
                    sh 'docker push kavyasekar00/myapp:latest'
                }
            }
        }

        stage('Deploy Container') {
            steps {
                sh '''
                docker stop myapp || true
                docker rm myapp || true
                docker run -d -p 8081:80 --name myapp kavyasekar00/myapp:latest
                '''
            }
        }
    }
}
