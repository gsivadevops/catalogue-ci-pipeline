pipeline {
  agent {
      label 'AGENT-1'
  }
  environment {
      COURSE = 'Jenkins'
  }
  options {
      timeout(time: 30, unit: 'MINUTES')
      disableConcurrentBuilds()
  }
  parameters {
      booleanParam(name: 'TOGGLE', defaultValue: true, description: 'Toggle this value')
  }
  stages {
      stage('Build') {
        steps {
          script{
            sh """
              echo 'Hello Build'
              sleep 10
              env
              echo "Hello ${PERSON}"
            """
          }
        }
      }
      stage('Test'){
        steps {
          script{
            echo 'Testing'
          }
        }
      }
      stage('Deploy'){
        input {
          message "Should we continue?"
          ok "Yes, We Should"
          submitter "alice,bob"
          parameters {
            string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
          }
        }
        steps {
          script{
            echo "Hello, ${PERSON}, nice to meet you."                    
            echo 'Deploying'
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



