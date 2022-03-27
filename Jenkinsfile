def buildStatus    = "FAILED"
def slackColor     = "warning"

pipeline {
  agent any
  stages {
    stage('Run Tests') {
      steps {
        sh './mvnw clean test'
        slackSend message: 'test passed'
      }
    }
  }
  post{
    success {
      script {
        buildStatus = "SUCCESS"
        slackColor = "good"
      }
    }
    cleanup {
      script {
        slackSend message: "color: "${slackColor}", message: "${buildStatus}" 
      }
    }
  }
}
