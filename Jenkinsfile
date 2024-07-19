pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Checkout code from SCM
                git url: 'https://github.com/Czech-King/test.git', branch: 'main'
            }
        }
        stage('Clean Up Old Docker Images') {
            steps {
                script {
                    // Remove all Docker images
                    sh 'docker rmi -f $(docker images -q) || true'
                }
            }
        }
        stage('Docker Build') {
            // Docker image build Stage
            steps {
                script {
                   sh 'docker build -t selvan/app:v2 .'
        }
    }
    
}
        stage ('Build Docker Image and push'){
            steps {
                script {
                   sh "docker login -u ${dockerusername} -p ${dockerpassword}"
                        }
                    }
}
}
}
