pipeline {
  agent { docker { image 'rapidfort/flaskapp' } }
  stages {
    stage('build') {
      steps {
        sh 'python3 test.py'
      }
    }
    stage('test') {
      steps {
        sh 'python3 test.py'
      }   
    }
  }
  post {
        always {
          junit 'test-reports/*.xml'
          cleanWs()
        }
      }
}
