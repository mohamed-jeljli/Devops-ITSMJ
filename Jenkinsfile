pipeline {
    agent any
    tools {
        maven 'M2_HOME'
    }
    
    stages {
        stage('clean') {
            steps {
                sh "mvn clean install"
            }
        }
        stage('Build') {
            steps {
                sh 'mvn package -Dspring.profiles.active=build'
            }
        }

       /*stage('SonarQube Analysis') {
    steps {
        withSonarQubeEnv('SonarQubeServer') {
            sh 'mvn sonar:sonar -Dsonar.projectKey=student-management'
        }
    }
}*/

    }
    post {
        success {
            archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
        }
    }
}

