pipeline {
    agent any
environment {

	DOCKER_REPO = 'boyca/test1'
	DOCKER_TAG = 'v1'
}
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
                   sh 'docker build -t app .'
                    sh 'docker images'
        }
    }
    
}
            stage('Push Docker Image') {
               steps {
                withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials-id', usernameVariable: 'dockerusername', passwordVariable: 'dockerpassword')]) {
                    script {
                        // Login to Docker Hub
                           sh "docker login -u ${dockerusername} -p ${dockerpassword}"
                        
                        // Push Docker image to Docker Hub
                           // sh 'docker tag app boyca/test1:v1'
                           // sh 'docker push boyca/test1:v1'
                        sh 'docker tag app ${DOCKER_REPO}:${DOCKER_TAG}'
                        sh 'docker push ${DOCKER_REPO}:${DOCKER_TAG}'
                    }
                }
            }
        }
}
}
