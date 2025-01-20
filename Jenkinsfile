pipeline {
    agent any

    environment {
        HOME_SONAR = tool 'sonar-scanner'
        }

    stages {
        }
         stage('NPM INSTALL') {
            steps {
                nodejs('node20') {
                    sh "npm install"
                }
            }
        }
        stage('Test') {
            steps {
                nodejs('node20') {
                sh "npm test"
               }
        }
        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('soanrserver') {
                    sh '''
                        $HOME_SONAR/bin/sonar-scanner \
                        -Dsonar.projectKey=nodePoject \
                        -Dsonar.projectName=NodeProject \
                        -Dsonar.sources=. \
                        -Dsonar.tests=. \
                        -Dsonar.test.inclusions=**/*.test.js \
                        -Dsonar.javascript.lcov.reportPaths=coverage/lcov.info
                       '''
            }
            }
        }
         stage('Quality gate') {
            steps {
              timeout(time: 1, unit: 'HOURS') {
                waitForQualityGate abortPipeline: false, credentialsId: 'SonarSecret'
                }
            }
        }

    
}
}