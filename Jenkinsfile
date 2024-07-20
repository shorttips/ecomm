pipeline {
    agent none

      environment {
        SLACK_CHANNEL = '#general' // Replace with your Slack channel
        SLACK_CREDENTIAL_ID = 'slack' // Replace with your Slack Credential ID
    }

    stages {
        stage('Pull code') {
            agent any
            steps {
                git branch: 'main', url: 'https://github.com/your-repo/your-project.git'
                sh 'echo "check"'
            }
        }
        stage('Slack Notification') {
            steps {
                agent any
                sh 'echo "slack notification"'
                slackSend channel: "${SLACK_CHANNEL}", color: 'good', message: "Code pushed to Github"
            }
        }
    }

     post 
     {
        success {
            slackSend channel: "${SLACK_CHANNEL}", color: 'good', message: "Build ${env.JOB_NAME} #${env.BUILD_NUMBER} succeeded"
        }
        failure {
            slackSend channel: "${SLACK_CHANNEL}", color: 'danger', message: "Build ${env.JOB_NAME} #${env.BUILD_NUMBER} failed"
        }
        unstable {
            slackSend channel: "${SLACK_CHANNEL}", color: 'warning', message: "Build ${env.JOB_NAME} #${env.BUILD_NUMBER} is unstable"
        }
        always {
            slackSend channel: "${SLACK_CHANNEL}", color: 'good', message: "Build ${env.JOB_NAME} #${env.BUILD_NUMBER} completed"
        }
     }
}

