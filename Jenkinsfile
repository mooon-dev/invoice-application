// pipeline {
//     agent any

//     environment {
//         DOCKER_CREDENTIALS = credentials('dockerHub')
//     }

//     stages {
//         stage('Clone Repository') {
//             steps {
//                 git branch: 'main', url: 'https://github.com/mooon-dev/invoice-application.git'
//             }
//         }

//         stage('Install Dependencies') {
//             steps {
//                 script {
//                     // Ensure npm dependencies are installed before building
//                     sh 'npm install'
//                 }
//             }
//         }

//         stage('Build Docker Images') {
//             steps {
//                 script {
//                     // Build the backend image
//                     sh 'docker build -t moonlovesmoon/mern-invoice-app:latest -f mern-invoice-app/Dockerfile .'
//                     // Build the frontend image
//                     sh 'docker build -t moonlovesmoon/client:latest -f client/Dockerfile .'
//                 }
//             }
//         }

//         stage('Push Docker Images') {
//             steps {
//                 script {
//                     // Push images to Docker Hub
//                     withDockerRegistry(credentialsId: 'dockerHub') {
//                         sh 'docker push moonlovesmoon/mern-invoice-app:latest'
//                         sh 'docker push moonlovesmoon/client:latest'
//                     }
//                 }
//             }
//         }

//         stage('Deploy using Docker Compose') {
//             steps {
//                 script {
//                     // Shut down any running containers
//                     sh 'docker-compose down'
//                     // Bring up the services in detached mode
//                     sh 'docker-compose up -d'
//                 }
//             }
//         }
//     }

// }














pipeline {
    agent any

    environment {
        DOCKER_CREDENTIALS = credentials('dockerHub') // Use Docker Hub credentials
    }

    stages {
        stage('Clone Repository') {
            steps {
                // Clone the main branch of the repository
                git branch: 'main', url: 'https://github.com/mooon-dev/invoice-application.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                script {
                    // Install npm dependencies for the main application
                    sh 'npm install'
                }
            }
        }

        stage('Build Docker Images') {
            steps {
                script {
                    // Build the backend Docker image
                    sh 'docker build -t moonlovesmoon/mern-invoice-app:latest -f mern-invoice-app/Dockerfile .'
                    // Build the frontend Docker image
                    sh 'docker build -t moonlovesmoon/client:latest -f client/Dockerfile .'
                }
            }
        }

        stage('Push Docker Images') {
            steps {
                script {
                    // Login and push Docker images to Docker Hub
                    withDockerRegistry(credentialsId: 'dockerHub') {
                        sh 'docker push moonlovesmoon/mern-invoice-app:latest'
                        sh 'docker push moonlovesmoon/client:latest'
                    }
                }
            }
        }

        stage('Deploy using Docker Compose') {
            steps {
                script {
                    // Shut down any existing containers
                    sh 'docker-compose down'
                    // Start the services in detached mode
                    sh 'docker-compose up -d'
                }
            }
        }
    }

    post {
        always {
            // Clean up the workspace to ensure no leftover files between builds
            cleanWs()
        }
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
