pipeline{
  agent any
  stages{
    stage('Checkout Out'){
      steps{
        git branch: 'main', url: 'https://github.com/emperor1245/test-django'
      }
    }
    stage('Login to ECR'){
      steps{
        withAWS(region: 'us-east-1', credentials: 'aws-creds'){
          powershell '''
          $password = aws ecr get-login-password --region us-east-1
          docker login --username AWS --password $password 314146306183.dkr.ecr.us-east-1.amazonaws.com/test
          '''
        }
      }
    }
    stage('Build docker image'){
      steps{
        powershell '''
        docker build -t test:django
        docker tag test:django 314146306183.dkr.ecr.us-east-1.amazonaws.com/test:django
        '''
      }
    }
    stage('Pushing image to ECR'){
      steps{
        powershell '''
        docker push 314146306183.dkr.ecr.us-east-1.amazonaws.com/test:django
        '''
      }
    }
  }
}
