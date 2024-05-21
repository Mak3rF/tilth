pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
		script{
	         echo 'Building..'
		 if(env.BRANCH_NAME == 'main'){
		   sh 'sudo docker build -f ~/jenkins-agent/jenkins-agent/workspace/prod.Dockerfile . -t tilth-app-prod'
		 }
		 else if(env.BRANCH_NAME == 'dev'){
		   sh 'pwd'
		   sh 'sudo docker build -f ~/jenkins-agent/jenkins-agent/workspace/dev.Dockerfile . -t tilth-app-dev'
		 }
		}
            }
        }
        stage('Deploy') {
             steps {
		script{
		 if(env.BRANCH_NAME == 'main'){
                  echo 'Deploying Prod..'
		  sh 'sudo docker rm -f tilth-prod || true'
		  sh 'sudo docker run -d -p 8080:80 --name tilth-prod tilth-app-prod'
	         }
		 else if (env.BRANCH_NAME == 'dev'){
		  echo 'Deploying Dev..'
		  sh 'sudo docker rm -f tilth-dev || true'
		  sh 'sudo docker run -d -p 8081:80 --name tilth-dev tilth-app-dev'
		 }
		}
            }
        }
    }
}
