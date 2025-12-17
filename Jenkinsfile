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
                sh '''
                    mvn sonar:sonar \
                      -Dsonar.projectKey=student-management \
                      -Dsonar.host.url=http://192.168.33.10:9000 \
                      -Dsonar.login=squ_96c0a10b5ca26ab414605985a8aad3e2e56ae963
                '''
            }
        }
    }
    post {
        success {
            archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
        }
    }
}

