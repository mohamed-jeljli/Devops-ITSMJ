pipeline {
  agent any
  tools { maven 'M2_HOME' }
  stages {
    stage('Build') {
      steps {
        sh 'mvn clean package -Dspring.profiles.active=build'
      }
    }
    stage('Push JAR to GitHub') {
    steps {
        sh '''
        git config user.email "jenkins@ci.local"
        git config user.name "Jenkins CI"
        git add target/*.jar
        git commit -m "Auto-commit built JAR"
        git push origin main
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


