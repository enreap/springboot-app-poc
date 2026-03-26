pipeline {
    agent any

    environment {
        KUBECONFIG = '/var/lib/jenkins/.kube/config'
        DOCKER_IMAGE = "enreapdevopsteam/springboot-app-poc"
        DOCKER_USERNAME = "enreapdevopsteam"
        DOCKER_PAT = "dckr_pat_rXL6w8JnJahrGp06JlL1TVPW-gk"  
        VERSION = "v1.${BUILD_NUMBER}"
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/enreap/springboot-app-poc.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                echo "Building Docker image..."
                // sh "docker build -t ${DOCKER_IMAGE}:${BUILD_NUMBER} ."
                sh "docker build -t ${DOCKER_IMAGE}:${VERSION} ."
            }
        }     
        stage('Push Docker Image') {
            steps {
                sh """
                    echo $DOCKER_PAT | docker login -u $DOCKER_USERNAME --password-stdin
                    docker push ${DOCKER_IMAGE}:${BUILD_NUMBER}
                """
            }
        }        

    }
}
