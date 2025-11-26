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
                sh '''
                git config user.email "jenkins@ci.local"
                git config user.name "Jenkins CI"

                # Add only the JAR file (since .gitignore ignores target/* except *.jar)
                git add target/*.jar

                # Commit if there are changes
                git diff --cached --quiet || git commit -m "Auto-commit built JAR from Jenkins"

                # Push to GitHub
                git push origin main
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



