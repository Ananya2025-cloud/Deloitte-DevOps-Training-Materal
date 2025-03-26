pipeline {
    agent any 
    parameters{
        string(name: 'VERSION', description: 'ENTER APP VERSION')
    }
    environment {
        AWS_ACCOUNT_ID= "586794440822"
        REGION="us-west-1"
        REPO_URL="${AWS_ACCOUNT_ID}.dkr.ecr.${REGION}.amazonaws.com/excelr"
        DOCKER_REGISTRY = 'docker.io'
        DOCKER_REGISTRY_CREDENTIALS= 'docker-creds'
    }
    stages {
        stage('Git Clone')
        {
            steps {
                echo "Cloning the GitHub Repository"
                git url: "Git URL", branch: 'main'
            }
        }
        stage('Docker Build')
        {
            steps {
                sh """ 
                docker build -t execlr-build-image :${VERSION}
                """
            }
        }
        stage('Image push to ECR')
        {
            steps{
                script {
                    withAWS(credentials: 'aws-creds')
                }
            }
        }
    }
}