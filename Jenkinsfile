pipeline {
  agent any
  tools { maven 'M2_HOME' }
  stages {
    stage('Build') {
      steps {
        sh 'mvn clean package -Dspring.profiles.active=build'
      }
    }
  }
  post {
    success {
      archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
    }
  }
}


