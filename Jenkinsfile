pipeline {
    agent any
        environment {
        // Define Docker repository and image name
        DOCKER_REPO = 'boyca/selvan/app:v2'
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
                   sh 'docker build -t selvan/app:v2 .'
        }
    }
    
}
        // stage ('Build Docker Image and push'){
        //     steps {
        //         script {
        //            sh "docker login -u ${dockerusername} -p ${dockerpassword}"
        //                 }
        //             }
// }
            stage('Push Docker Image') {
               steps {
                withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials-id', usernameVariable: 'dockerusername', passwordVariable: 'dockerpassword')]) {
                    script {
                        // Login to Docker Hub
                           sh "docker login -u ${dockerusername} -p ${dockerpassword}"
                        
                        // Push Docker image to Docker Hub
                        sh 'docker push ${DOCKER_REPO}'
                    }
                }
            }
        }
}
}
