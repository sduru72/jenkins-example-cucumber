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
      cucumber buildStatus: 'null', customCssFiles: '', customJsFiles: '', failedFeaturesNumber: -1, failedScenariosNumber: -1, failedStepsNumber: -1, fileIncludePattern: 'target/cucumber.json', pendingStepsNumber: -1, skippedStepsNumber: -1, sortingMethod: 'ALPHABETICAL', undefinedStepsNumber: -1
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
