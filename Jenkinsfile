pipeline {
	agent any
  stages 
  {
    stage('Docker Build') 
    {
    	agent any
      steps {
        sh 'echo "Building Docker Image..."'
      	sh 'docker build -t orabitbul/latest .'
        sh 'docker images'
      }
    }
    stage('Push Image to ECR') 
    {
    	agent any
      steps {
        sh 'echo "Pushing Image to ECR..."'
        sh 'docker push 132737078540.dkr.ecr.us-east-1.amazonaws.com/flask_jenkinsapp'
      }
    }
  }
}
