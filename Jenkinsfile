def buildStatus    = "FAILED"
def slackColor     = "warning"

pipeline {
  agent any
  triggers{
    cron 'H 2,16 * * *'
  }
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
        slackSend color: "${slackColor}", message: "${buildStatus}", `${env.JOB_NAME}`
      }
    }
  }
}
