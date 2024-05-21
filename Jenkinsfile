pipeline {
    agent any
    stages {
	stage('Remove Old Repo'){
	    steps{
		sh "cd development"
		sh "rm -rf tilth"
	    }

	}
        stage('Clone Repo') {
            steps {
                script {
		 sh "mkdir tilth"
		 sh "cd tilth"
                 git credentialsId: 'jenkins-github', url: 'https://github.com/mak3rf/tilth.git'
		 sh "git checkout main"
		}
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}
