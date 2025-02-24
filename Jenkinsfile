pipeline {
    agent any

    stages {
        stage('Build & Tag Docker Image') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                        sh "docker build -t nishargsoni/adservice:latest ."
                    }
                }
            }
        }
        
        stage('Push Docker Image') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                        sh "docker push nishargsoni/adservice:latest "
                    }
                }
            }
        }
    }
    post {
        success {
            build job: 'CD-Pipeline-Deploy', wait: false
        }
    }
}
