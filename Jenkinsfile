pipeline {
    agent none

      environment {
        SLACK_CHANNEL = '#general' // Replace with your Slack channel
        SLACK_CREDENTIAL_ID = 'slack' // Replace with your Slack Credential ID
    }

    stages {
        stage('Pull code') {
            steps {
                git branch: 'main', url: 'https://github.com/your-repo/your-project.git'
            }
        }
        stage('Slack Notification') {
            steps {
                sh 'echo "slack notification"'
                slackSend channel: "${SLACK_CHANNEL}", color: 'good', message: "Code pushed to Github"
            }
        }
    }
}

