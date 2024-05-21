pipeline {
    agent any
    stages {
        stage('Clone Repo') {
            steps {
              git branch: 'main', credentialsId: 'jenkins-github', url: 'https://github.com/mak3rf/tilth.git'
            }
        }
        stage('Build') {
            steps {
                echo 'Building..'
		sh 'sudo docker build . -t tilth-app-prod'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying..'
		sh 'sudo docker run -d -p 8080:80 tilth-app-prod'
            }
        }
    }
}
