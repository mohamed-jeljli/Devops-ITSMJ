pipeline {
    agent any

    tools {
        maven 'M2_HOME'
    }

    environment {
        DOCKER_IMAGE = "1tsmj/Devops-ITSMJ:latest"
    }

    stages {
        stage('Code Checkout') {
            steps {
                echo "Checking out code from GitHub..."
                git branch: 'main',
                    url: 'https://github.com/mohamed-jeljli/Devops-ITSMJ.git/'
            }
        }

        stage('Code Build') {
            steps {
                echo "Building project with Maven..."
                sh 'mvn install -Dmaven.test.skip=true'
            }
        }

        stage('Maven Package') {
            steps {
                echo "Packaging project..."
                sh 'mvn package -Dmaven.test.skip=true'
            }
        }

    stage('SonarQube Analysis') {
                    steps {
                        withSonarQubeEnv('SonarQubeServer') {
                        sh 'mvn sonar:sonar -Dsonar.projectKey=student-management'
                            }
                    }
              }

        stage('Docker Login') {
            steps {
                echo "Logging into Docker Hub..."
                withCredentials([usernamePassword(credentialsId: 'Docker-cred', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh 'echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin'
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                echo "Building Docker image..."
                sh "docker build -t $DOCKER_IMAGE ."
            }
        }

        stage('Push Docker Image') {
            steps {
                echo "Pushing Docker image to Docker Hub..."
                sh "docker push $DOCKER_IMAGE"
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                echo "Deploying MySQL and Spring Boot app to Kubernetes..."
                sh "kubectl apply -f k8s/mysql-deployment.yaml"
                sh "kubectl apply -f k8s/app-deployment.yaml"
            }
        }
    }

    post {
        always {
            echo "====== Pipeline finished ======"
        }
        success {
            echo "===== Pipeline executed successfully ====="
        }
        failure {
            echo "====== Pipeline execution failed ======"
        }
    }
}
