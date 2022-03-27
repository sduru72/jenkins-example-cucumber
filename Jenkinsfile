def buildStatus    = "FAILED"
def slackColor     = "warning"
def slackChannelID = 'C035MHTT1SR'

pipeline {
  agent any
  stages {
    stage('Run Tests') {
      steps {
        sh './mvnw clean test'
      }
    }
  }
  post {
        always {
            script {
                junit skipPublishingChecks: true, testResults: 'junit.xml'
            }
        }
        success {
            script {
                buildStatus = "SUCCESS"
                slackColor = "good"
            }
        }
        cleanup {
            script {
                slackSend channel: "${slackChannelID}", color: "${slackColor}", message: "*${buildStatus}*: `${env.JOB_NAME}` *#${env.BUILD_NUMBER}* \n<${env.BUILD_URL}/console|Console Log>"
            }
        }
    }
}
