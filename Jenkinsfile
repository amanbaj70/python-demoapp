pipeline {
    agent any

    stages {
        stage('Git checkout') {
            steps {
                git 'https://github.com/amanbaj70/python-demoapp.git'
            }
        }
        
        stage('Docker build') {
            steps {
                sh 'make image'
            }
        }
        
        stage('Docker push') {
            steps {
                withDockerRegistry(credentialsId: 'b8764920-1a6f-4c6d-a4a0-19200c0f100c') {
                 sh 'make push'
                }
            }
        }
        
        stage('Docker deploy') {
            steps {
                sh 'docker run --rm -d -p 5000:5000 amanbajpai/python-demoapp:latest'
            }
        }
    }
    
    post{
        always{
            echo "========always========"
        }
        success{
            echo "========pipeline executed successfully ========"
        }
        failure{
            echo "========pipeline execution failed========"
        }
    }
}