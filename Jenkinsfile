pipeline {
    agent any
    stages {
        stage('Clone Repo') {
            steps {
                script {
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
