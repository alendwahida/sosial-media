pipeline {
    agent {
        node {
            label 'agent1'
        }
    }
    stages {
        stage ('git') {
            steps {
                sh 'git log'
            }
        }
        stage ('ECR Login') {
            steps {
                sh 'aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 128150454185.dkr.ecr.us-east-1.amazonaws.com'
            }
        }
        stage ('Docker Build') {
            steps {
                sh 'docker ps'
            }
        }
        stage ('docker Push ECR') {
            steps {
                sh 'docker images'
            }
        }
        stage ('Deployment Images EKS') {
            steps {
                sh "docker version"
            }
        }
    }
}
