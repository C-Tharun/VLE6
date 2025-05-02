pipeline {
    agent any  // This will run on any available agent (e.g., master or worker node)
    
    tools {
        maven 'Maven 3.8.1'  // This ensures Maven 3.8.1 is available on the Jenkins agent
    }

    environment {
        DOCKER_IMAGE = "yourdockerhubusername/sample-java-app:${BUILD_NUMBER}"  // Docker image name with Jenkins build number
    }

    stages {
        stage('Checkout Code') {
            steps {
                // Checkout the code from GitHub
                git 'https://github.com/your-username/sample-java-app.git'
            }
        }

        stage('Build with Maven') {
            steps {
                // Build the project with Maven
                sh 'mvn clean package'
            }
        }

        stage('Build Docker Image') {
            steps {
                // Build Docker image
                sh 'docker build -t $DOCKER_IMAGE .'
            }
        }

        stage('Push to Docker Hub') {
            steps {
                // Push the Docker image to Docker Hub
                withDockerRegistry([credentialsId: 'docker-hub-creds']) {
                    sh 'docker push $DOCKER_IMAGE'
                }
            }
        }
    }
}
