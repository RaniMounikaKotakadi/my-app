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
                     archiveArtifacts(artifacts: "build/**/*")
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
                withCredentials(sshUserPrivateKey[(credentialsId: 'aws_ssh_credential', usernameVariable: 'SSH_USERNAME', keyFileVariable: 'SSH_PRIVATE_KEY')]) {
                    sh 'eval $(ssh-agent -s)'
                    sh "ssh-add ${SSH_PRIVATE_KEY}"
                    sh "ssh -oStrictHostKeyChecking=no ${SSH_USERNAME}@$deployment_server ls /"
                }
            }
        }
    }
    post {
        always {
            sh 'ssh-add -D || true'
            sh 'ssh-agent -k || true'
        }
    }
}
