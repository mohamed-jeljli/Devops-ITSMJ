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
              -Dsonar.host.url=http://192.168.1.12:9000 \
              -Dsonar.login=SONAR-QUBE-TOKEN
        '''
    }
}

        }
    }
    post {
        success {
            archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
        }
    }
}





