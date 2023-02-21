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
    }
}
