pipeline {
    agent {
    label 'WorkerNode1'
      }
    tools {
     nodejs 'Node'
      }

    stages {
        }
         stage('NPM INSTALL') {
            steps {
                sh "npm install"
            }
        }
        stage('NPM BUILD') {
            steps {
                sh "npm run"
            }
        }
        stage('NPM START') {
            steps {
                sh "npm start"
            }
        }
    
}
