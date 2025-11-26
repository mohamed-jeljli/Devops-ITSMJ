pipeline{
    agent any
    tools {
        maven 'M2_HOME'
    }
    stages {
        stage('GIT'){
            steps{
                git branch: 'main',
                url: 'https://github.com/mohamed-jeljli/Devops-ITSMJ.git',
                credentialsId: '52eae079-e90f-48cd-af39-2c5a205b6082'

            }
        }
    }
