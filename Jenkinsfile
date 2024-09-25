pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Clone the Git repository
                git url: 'https://github.com/chirag1207/g01461345swe645-assignment02', branch: 'main'
            }
        }

        stage('Build Docker Image') {
            steps {
                // Build the Docker image using the Dockerfile
                script {
                    docker.build('g01461345-swe645-assignment-02')
                }
            }
        }

        stage('Push Docker Image to Local Registry') {
            steps {
                // Push the Docker image to your local Docker registry
                script {
                    docker.withRegistry('http://localhost:5000') {
                        docker.image('g01461345-swe645-assignment-02').push('latest')
                    }
                }
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                // Apply Kubernetes deployment and service YAML files
                sh 'kubectl apply -f k8s/deployment.yaml'
                sh 'kubectl apply -f k8s/service.yaml'
            }
        }
    }

    post {
        always {
            // Clean up workspace after build
            cleanWs()
        }
    }
}
