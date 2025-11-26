pipeline {
    agent any

    tools {
        maven 'M2_HOME'   // Make sure Maven is configured in Jenkins under this name
    }

    stages {
        stage('Build JAR') {
            steps {
                sh 'mvn clean package -Dspring.profiles.active=build'
            }
        }

        stage('Archive Artifact') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }

       stage('Push JAR to GitHub') {
    steps {
        withCredentials([usernamePassword(credentialsId: '52eae079-e90f-48cd-af39-2c5a205b6082	',
                                         usernameVariable: 'mohamed-jeljli',
                                         passwordVariable: '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
')]) {
            sh '''
            git config user.email "jenkins@ci.local"
            git config user.name "Jenkins CI"
            git add target/*.jar
            git diff --cached --quiet || git commit -m "Auto-commit built JAR from Jenkins"
            git push https://$GIT_USER:$GIT_PASS@github.com/mohamed-jeljli/Devops-ITSMJ.git main
            '''
        }
    }
}


    post {
        failure {
            echo 'Build failed — check Maven logs!'
        }
        success {
            echo 'Build succeeded — JAR archived and pushed to GitHub.'
        }
    }
}



