def buildStatus    = "FAILED"
def slackColor     = "warning"
def slackChannelID = 'C035MHTT1SR'

pipeline {
  agent any
  triggers{
    cron 'H 2,16 * * *'
  }
  stages {
    stage('Run Tests') {
      steps {
        sh './mvnw clean test'
      }
    }
  }
  post{
    always{
      junit '**/surefire-reports/*.xml'
    }
    success {
      script {
        buildStatus = "SUCCESS"
        slackColor = "good"
      }
    }
    cleanup {
      script {
        slackSend channel: "C035MHTT1SR", color: "${slackColor}", message: "*${buildStatus}*: `${env.JOB_NAME}` *#${env.BUILD_NUMBER}* \n<${env.BUILD_URL}/console|Console Log>"
      }
    }
  }
}
