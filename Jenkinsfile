pipeline {
    agent any
    stages {
        stage('Clone Repo') {
            steps {
	      script{
	       if(env.BRANCH_NAME == 'dev'){
	         git branch: 'dev', credentialsId: 'jenkins-github', url: 'https://github.com/mak3rf/tilth.git'
	       }
	       else if(env.BRANCH_NAME == 'main'){
	         git branch: 'main', credentialsId: 'jenkins-github', url: 'https://github.com/mak3rf/tilth.git'
	       }
	      }
            }
        }
        stage('Build') {
            steps {
		script{
	         echo 'Building..'
		 if(env.BRANCH_NAME == 'main'){
		   sh 'sudo docker build ~/jenkins-agent/jenkins-agent/workspace/prod.Dockerfile -t tilth-app-prod'
		 }
		 else if(env.BRANCH_NAME == 'dev'){
		   sh 'sudo docker build ~/jenkins-agent/jenkins-agent/workspace/dev.Dockerfile -t tilth-app-dev'
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
