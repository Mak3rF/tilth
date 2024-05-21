pipeline {
    agent any
    stages {
        stage('Clone Repo') {
            steps {
	      if(env.BRANCH_NAME == 'dev'){
	        git branch: 'dev', credentialsId: 'jenkins-github', url: 'https://github.com/mak3rf/tilth.git'
	      }
	      else if(env.BRANCH_NAME == 'main'){
	        git branch: 'main', credentialsId: 'jenkins-github', url: 'https://github.com/mak3rf/tilth.git'
	      }
            }
        }
        stage('Build') {
            steps {
                echo 'Building..'
		sh 'sudo docker build ~/jenkins-agent/jenkins-agent/workspace -t tilth-app-prod'
            }
        }
        stage('Deploy') {
             steps {
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
