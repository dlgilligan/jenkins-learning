pipeline {
    agent any
    options {
        skipStagesAfterUnstable()
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying'
            }
        }
    }

    post {
        failure {
            slackSend channel: '#ops',
                      color: 'good',
                      message: '${currentBuild.fullDisplayName} succeeded'
                         
        }

        success {
            slackSend channel: '#ops',
                      color: 'good',
                      message: '${currentBuild.fullDisplayName} failed'
        }

        always {
            archiveArtifacts artifacts: 'build/libs/**/*.jar', fingerprint: 'true'
            junit 'build/libs/**/*.xml'
        }
    }
}
