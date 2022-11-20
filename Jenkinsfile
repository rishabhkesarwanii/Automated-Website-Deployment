pipeline {
    agent any
    stages {
        stage('Build Img'){
            steps{
            sh 'printenv'
            }
        }
        stage('Publish ECR'){
            steps{
                withEnv (["AWS_ACCESS_KEY_ID=${env.AWS_ACCESS_KEY_ID}","AWS_SECRET_ACCESS_KEY=${env.AWS_SECRET_ACCESS_KEY}","AWS_DEFAULT_REGION=${env.AWS_DEFAULT_REGION}"])
                {
                    sh 'docker login -username AWS -password-stdin $(aws ecr get-login-password --region ap-south-1) public.ecr.aws/z5t7j9t8'
                    sh 'docker build -t jenkis-docker-image .'
                    sh 'docker tag jenkis-docker-image:latest public.ecr.aws/z5t7j9t8/jenkis-docker-image:""$BUILD_ID""'
                    sh 'docker push public.ecr.aws/z5t7j9t8/jenkis-docker-image:""$BUILD_ID""'
                }
            }
        }
    }
}
