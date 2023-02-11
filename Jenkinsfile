pipeline {
	agent any
  stages 
  {
    stage('Docker Build') 
    {
    	agent any
      steps {
        sh 'echo "Building Docker Image..."'
      	sh 'docker build -t flask-app:1.0 .'
        sh 'docker images'
      }
    }
    stage('Push Image to ECR') 
    {
    	agent any
      steps {
        sh 'echo "Pushing Image to ECR..."'
        sh 'aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 132737078540.dkr.ecr.us-east-1.amazonaws.com'
	sh 'docker tag flask-app:1.0 132737078540.dkr.ecr.us-east-1.amazonaws.com/flask_jenkinsapp:1.0'
	sh 'docker push 132737078540.dkr.ecr.us-east-1.amazonaws.com/flask_jenkinsapp:1.0'
      }
    }
    stage('SSH to App Server') 
    {
    	agent any
      steps {
        sh 'echo "Connecting to APP server..."'
	sh 'sudo chmod 600 ~/.ssh/web1-key.pem'
      	sh '''
        ssh -i ~/.ssh/web1-key.pem ubuntu@54.234.100.234
        "aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 132737078540.dkr.ecr.us-east-1.amazonaws.com; 
        docker pull 132737078540.dkr.ecr.us-east-1.amazonaws.com/flask_jenkinsapp:1.0;
        docker run -itd -p 5000:5000 --name final-cont 132737078540.dkr.ecr.us-east-1.amazonaws.com/flask_jenkinsapp:1.0;
        curl  127.0.0.1:5000"
        '''
      }
    }
  }
}
