#!/usr/bin/env groovy
pipeline {
    agent any
    triggers { pollSCM('H/5 * * * *') }
    stages {
        stage('Build') {
            steps {
                sh './mvnw clean package'
            }
        }
    }
    post {
        always {
            junit '**/target/surefire-reports/TEST-*.xml'
        }
        success {
            archiveArtifacts 'target/*.jar'
        }
        changed {
            emailext attachLog: true, body: ''Please go to ${BUILD_URL} and verify the build'', compressLog: true, recipientProviders: [upstreamDevelopers(), requestor()], subject: ''Job \'$(JOB_NAME)\' (Build ${BUILD_NUMBER}) ${currentBuild.result}''
        }
    }
}
