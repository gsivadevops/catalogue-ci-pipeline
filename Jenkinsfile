pipeline {
  agent {
      label 'AGENT-1'
  }
  environment {
      appVersion = ''
      REGION = "us-east-1"
      ACCOUNT_ID = "020027209432"
      PROJECT = "roboshop"
      COMPONENT = "catalogue"
  }
  options {
      timeout(time: 30, unit: 'MINUTES')
      disableConcurrentBuilds()
  }
  stages {
      stage('Read Package.json') {
        steps {
          script{
            def packageJson = readJSON file: 'package.json'
            appVersion = packageJson.version
            echo "Package Version: ${appVersion}"
          }
        }
      }
      stage('Install Dependencies') {
        steps {
          script{
            sh """
              npm install              
            """
          }
        }
      }      
      stage('Docker Build') {
          steps {
              script {
                  withAWS(credentials: 'aws-creds', region: ${REGION}) {
                      sh """
                          aws ecr get-login-password --region ${REGION} | docker login --username AWS --password-stdin ${ACCOUNT_ID}.dkr.ecr.us-east-1.amazonaws.com
                          docker build -t ${ACCOUNT_ID}.dkr.ecr.us-east-1.amazonaws.com/${PROJECT}/${COMPONENT}:${appVersion} .
                          docker push ${ACCOUNT_ID}.dkr.ecr.us-east-1.amazonaws.com/${PROJECT}/${COMPONENT}:${appVersion}
                      """
                  }
              }
          }
      }
  }
  post {
    always {
      echo 'I will always say Hello Again!'
      deleteDir()
    }
    success {
      echo 'Hello Success'
    }
    failure {
      echo 'Hello Failure'
    }
  }
}



