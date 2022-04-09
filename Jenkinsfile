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
                sh 'printenv'
            }
        }
        stage ('ECR Login') {
            steps {
                sh 'aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 128150454185.dkr.ecr.us-east-1.amazonaws.com'
            }
        }
        stage ('Docker Build') {
            steps {
                sh 'docker build -t sosialmedia .'
            }
        }
        stage ('docker Push ECR') {
            steps {
                sh 'docker tag sosialmedia:latest 128150454185.dkr.ecr.us-east-1.amazonaws.com/sosialmedia:$GIT_COMMIT'
                sh 'docker push 128150454185.dkr.ecr.us-east-1.amazonaws.com/sosialmedia:$GIT_COMMIT'
                sh 'docker tag 128150454185.dkr.ecr.us-east-1.amazonaws.com/sosialmedia:$GIT_COMMIT 128150454185.dkr.ecr.us-east-1.amazonaws.com/sosialmedia:latest'
            }
        }
        stage ('Deployment Images EKS') {
            steps {
                sh "docker version"
            }
        }
    }
}
