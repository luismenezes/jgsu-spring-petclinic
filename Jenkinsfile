pipeline {
    agent any
    stages {
            stage ('Build') {
                    steps {
                            sh './mvnw clean package'
                    }
            }
    }
    post {
        always {
            junit '**/target/surefire-reports/TEST-*.xml'
            archiveArtifacts 'target/*.jar'
        }
            success {
                    archiveArtifacts artifacts: 'target/*.jar', followSymlinks: false
        }
    }
}
