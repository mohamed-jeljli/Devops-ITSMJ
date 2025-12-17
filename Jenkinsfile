pipeline {
    agent any

    tools {
        maven 'M2_HOME'
    }

    stages {
        stage('Code Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/OumaymaBrineg/DEVOPS_PROJECT.git'
                    // If private repo, add: credentialsId: 'jenkins-example-github-pat'
            }
        }

        stage('Code Build') {
            steps {
                sh 'mvn install -Dmaven.test.skip=true'
            }
        }

         stage('mvn Package') {
                    steps {
                        sh 'mvn package -Dmaven.test.skip=true'
                    }
                }
    }

    post {
        always {
            echo "======always======"
        }
        success {
            echo "=====pipeline executed successfully ====="
        }
        failure {
            echo "======pipeline execution failed======"
        }
    }
}
