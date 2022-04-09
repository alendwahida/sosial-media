pipeline {
    agent {
        node {
            label 'agent1'
        }
    }
    environment {
        AWS_REGION = 'us-east-1'
        AWS_ID = '128150454185'
        PROJECT_NAME = 'sosialmedia'
    }
    stages {
        stage ('git') {
            steps {
                dir('A') {
                    git url: 'https://github.com/alendwahida/sosial-media.git', credentialsId: '1'
                }
                dir('B') {
                    git url: 'https://github.com/alendwahida/gitops-test.git', credentialsId: '1'
                }
                sh 'ls'
                sh 'git log'
                sh 'printenv'
            }
        }
        stage ('ECR Login') {
            steps {
                sh 'aws ecr get-login-password --region ${AWS_REGION} | docker login --username AWS --password-stdin ${AWS_ID}.dkr.ecr.${AWS_REGION}.amazonaws.com'
            }
        }
        stage ('Docker Build') {
            steps {
                sh 'docker build -t ${PROJECT_NAME} .'
            }
        }
        stage ('Push ECR') {
            steps {
                sh 'docker tag ${PROJECT_NAME}:latest ${AWS_ID}.dkr.ecr.us-east-1.amazonaws.com/${PROJECT_NAME}:$GIT_COMMIT'
                sh 'docker push ${AWS_ID}.dkr.ecr.${AWS_REGION}.amazonaws.com/${PROJECT_NAME}:$GIT_COMMIT'
                sh 'docker tag ${AWS_ID}.dkr.ecr.${AWS_REGION}.amazonaws.com/${PROJECT_NAME}:$GIT_COMMIT ${AWS_ID}.dkr.ecr.${AWS_REGION}.amazonaws.com/${PROJECT_NAME}:latest'
            }
        }
        stage ('Manifest Image Version into deployment.yaml') {
            steps {
                sh '$GIT_COMIT'
            }
        }
    }
}
