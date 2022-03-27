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
        slackSend message: "color: "${slackColor}", message: "*${buildStatus}*: `${env.JOB_NAME}` *#${env.BUILD_NUMBER}* \n<${env.BUILD_URL}/console|Console Log>" 
      }
    }
  }
}
