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
                      -Dsonar.login=sqa_2e8090b8e8ceba6142fdfbd839017ccf1bd6a98a
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

