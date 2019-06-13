pipeline {
    agent any

    environment {
        CI = 'true' 
    }
    stages {

        stage('Prepare') {
            steps {
                sh 'npm install'
            }
        }

        stage('CodeTest') {
            steps {
                sh 'echo "code testing"'
            }
        }

        stage('Build') {
            steps {
                sh 'npm run build'
                script { 
                     archiveArtifacts(artifacts: "build/*")
                }
            }
        }

        stage('Test') {
            steps {
                sh 'npm run test'
            }
        }

        stage('deploy') {
            steps {
                sh 'echo deploying'
            }
        }
    }
}
