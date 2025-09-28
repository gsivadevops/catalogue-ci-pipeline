pipeline {
  agent {
      label 'AGENT-1'
  }
  environment {
      appVersion = ''
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



