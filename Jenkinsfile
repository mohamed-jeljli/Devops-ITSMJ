pipeline {
    agent any
    tools {
        maven 'M2_HOME'
    }
    stages {
        stage('Build') {
            steps {
                sh 'mvn package -Dspring.profiles.active=build'
            }
        }

        stage('MVN SONARQUBE') {
            steps {
                sh 'mvn sonar:sonar'
            }
        }
    }
    post {
        success {
            archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
        }
    }
}





