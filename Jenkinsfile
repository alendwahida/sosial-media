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
                sh 'aws ecr'
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
