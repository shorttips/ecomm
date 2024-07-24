pipeline {
    agent any //declares the app or tool used by jenkins to execute the commands

      environment {
        // Slack environment variables
        SLACK_CHANNEL = '#general' // Replace with your Slack channel
        SLACK_CREDENTIAL_ID = 'slack' // Replace with your Slack Credential ID

         // Define SonarQube environment variables
        SONARQUBE_URL = 'http://13.127.214.243:9000'  
        SONARQUBE_CREDENTIALS = 'sq1-ecomm' 
    }

    stages {
        //Pulls data from remote VCM and triggers the pipeline
        stage('Checkout') {
            steps {
                sh 'echo "Pulling Code from Github VCM"'
                git branch: 'main', url: 'https://github.com/shorttips/ecomm.git'
            }
        }


        stage('Slack Notification') {
            steps {
                sh 'echo "slack notification"'
                slackSend channel: "${SLACK_CHANNEL}", color: 'good', message: "Code was pushed to Github"
            }
        }

        /*
        stage('SonarQube Analysis') {
            steps {
                sh 'echo "Sonarqube Analysis"'
            }
        }
        */

        stage('Build') {
            steps {
                sh 'echo "Build Stage...."'
                nodejs(nodeJSInstallationName: 'node 22.5.1') {
                    sh 'npm -v'
                    sh 'npm install'
                    sh 'npm build'
                }
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





/*
pipeline {
    agent any //declares the app or tool used by jenkins to execute the commands

    stages {
        //Pulls data from remote VCM and triggers the pipeline
        stage('Checkout') {
            steps {
                sh 'echo "Pulling Code from Github"'
                git branch: 'Branch-integrated-with-pipeline', url: 'https://url/to/repo'
            }
        }
        
        stage('Build') {
            steps {
                sh 'echo "Build Stage"'
                nodejs(nodeJSInstallationName: 'name given in the earlier step') {
                    //npm commands to build the application
                    
                }
            }
    }
}
*/
