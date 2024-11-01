pipeline {
    agent any

    environment {
        DOCKER_HUB_REPO = 'nbest5175/my-app'         // Your Docker Hub repo
        DOCKER_CREDENTIALS_ID = 'docker-hub-credentials' // Credentials ID in Jenkins
    }

    stages {
        stage('Install Dependencies') {
            steps {
                script {
                    // Installs necessary Node.js dependencies
                    sh 'npm install'
                }
            }
        }

        stage('Build') {
            steps {
                script {
                    // Placeholder build step for Node.js app, can be customized
                    echo 'Building the application...'
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    // Runs any tests specified in the Node.js project
                    sh 'npm test'
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    // Build the Docker image for the app
                    def image = docker.build("${DOCKER_HUB_REPO}:latest")
                }
            }
        }
        
        stage('Login to Docker Hub') {
            steps {
                script {
                    // Login to Docker Hub using Jenkins credentials
                    docker.withRegistry('https://registry.hub.docker.com', "${DOCKER_CREDENTIALS_ID}") {
                        echo "Logged in to Docker Hub"
                    }
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    // Push the Docker image to Docker Hub
                    def image = docker.image("${DOCKER_HUB_REPO}:latest")
                    image.push()
                }
            }
        }
    }
}
