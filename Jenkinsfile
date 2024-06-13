pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "zaffarwani/farmly:v1"
        //REGISTRY_CREDENTIALS = 'docker-hub-credentials' 
    }
    stages {
      stage('Build Docker Image') {
            steps {
                script {
                    docker.build(DOCKER_IMAGE)
                }
            }
        }
      stage('Run Docker Container') {
            steps {
                script {
                    sh 'docker run -d -p 80:80 --name farmly-container ' + DOCKER_IMAGE
                }
            }
        }
    }
    post {
        always {
            // Clean up Docker containers
            script {
                sh 'docker stop farmly-container || true'
                sh 'docker rm farmly-container || true'
                sh 'docker rmi ' + DOCKER_IMAGE + ' || true'
            }
        }
    }
}
