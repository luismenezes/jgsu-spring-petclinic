
#!/usr/bin/env groovy
// shebang tells most editors to treat as groovy (syntax highlights, formatting, etc)

pipeline {
    agent any
    stages {
        stage ('Checkout') {
		    steps {
			    git branch: 'main', url: 'https://github.com/luismenezes/jgsu-spring-petclinic.git'
		    }
	    }
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
