pipeline {
	agent any
  stages 
  {
    stage('Docker Build') 
    {
    	agent any
      steps {
        sh 'echo "Building Docker Image..."'
      	sh 'docker build -t orabitbul/v1 .'
        sh 'docker images'
      }
    }
    stage('Push Image to ECR') 
    {
    	agent any
      steps {
        sh 'echo "Pushing Image to ECR..."'
        sh 'aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 132737078540.dkr.ecr.us-east-1.amazonaws.com'
	sh 'docker tag orabitbul/v1:latest 132737078540.dkr.ecr.us-east-1.amazonaws.com/flask_jenkinsapp:latest'
	sh 'docker push 132737078540.dkr.ecr.us-east-1.amazonaws.com/flask_jenkinsapp:latest'
      }
    }
  }
}
