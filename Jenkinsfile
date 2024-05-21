pipeline {
    agent any
    stages {
        stage('Clone Repo') {
            steps {
              git branch: 'main', credentialsId: 'jenkins-github', url: 'https://github.com/mak3rf/tilth.git'
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
