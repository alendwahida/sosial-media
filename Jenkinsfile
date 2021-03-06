pipeline {
    agent {
        node {
            label 'agent1'
        }
    }
    stages {
        stage ('ECR Login') {
            steps {
                sh 'aws ecr get-login-password --region $AWS_REGION | docker login --username AWS --password-stdin $AWS_ID.dkr.ecr.$AWS_REGION.amazonaws.com'
            }
        }
        stage ('Docker Build') {
            steps {
                sh 'docker build -t $PROJECT_NAME .'
            }
        }
        stage ('Push ECR') {
            steps {
                sh 'docker tag $PROJECT_NAME:latest $AWS_ID.dkr.ecr.us-east-1.amazonaws.com/$PROJECT_NAME:$GIT_COMMIT'
                sh 'docker push $AWS_ID.dkr.ecr.$AWS_REGION.amazonaws.com/$PROJECT_NAME:$GIT_COMMIT'
                sh 'docker tag $AWS_ID.dkr.ecr.$AWS_REGION.amazonaws.com/$PROJECT_NAME:$GIT_COMMIT $AWS_ID.dkr.ecr.$AWS_REGION.amazonaws.com/$PROJECT_NAME:latest'
            }
        }
        stage ('Manifest Image Version Repository') {
            steps {
                echo "Update manifest jobs"
                build job: '001-staging-updatemanifest-sosialmedia', 
                    parameters: [
                        string(name: 'IMAGE_TAG', value: env.GIT_COMMIT),
                        string(name: 'PROJECT_NAME', value: env.PROJECT_NAME)
                    ]
            }
        }
    }
}
