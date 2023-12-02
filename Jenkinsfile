/* groovylint-disable LineLength */
pipeline {
  agent any
  environment {
    AWS_ACCESS_KEY_ID = ''
    AWS_SECRET_ACCESS_KEY = ''
    AWS_DEFAULT_REGION = 'ap-south-1'
    AWS_S3BUCKET_NAME = ''
    CLOUD_FRONT_DISTRIBUTION = ''
 }
  stages {
    stage('Build') {
      steps {
        sh('sh ./build.sh')
      }
    }
    stage('Test') {
      steps {
        sh('echo test')
      }
    }
    stage('Deploy to S3') {
      steps {
        sh "aws configure set region ${AWS_DEFAULT_REGION}"
        sh "aws configure set aws_access_key_id ${AWS_ACCESS_KEY_ID}"
        sh "aws configure set aws_secret_access_key ${AWS_SECRET_ACCESS_KEY}"
        sh("aws s3 cp build/web s3://${AWS_S3BUCKET_NAME}/ --recursive --region ${AWS_DEFAULT_REGION}");
        sh("echo Deployment completed successfully.")
        sh("echo Invalidating cache ....")
        sh("aws cloudfront create-invalidation --distribution-id ${CLOUD_FRONT_DISTRIBUTION}  --paths /index.html /error.html")
        sh("echo Invalidated cache successfully...")
     }
    }
  }
}