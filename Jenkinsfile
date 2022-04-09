pipeline {
    agent {
        node {
            label 'agent1'
        }
    }
    stages {
        stage('docker Version') {
            steps {
                sh 'docker version'
            }
        }
        stage ('aws ecr') {
            steps {
                sh("eval \$(aws ecr get-login --no-include-email | sed 's|https://||')")
            }
        }
        stage ('docker Build') {
            steps {
                sh 'docker ps'
            }
        }
        stage ('docker Push ECR') {
            steps {
                sh 'docker images'
            }
        }
        stage ('deployment Images EKS') {
            steps {
                sh "docker version"
            }
        }
    }
}
