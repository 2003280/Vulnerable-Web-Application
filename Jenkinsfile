pipeline {
	agent any
	stages {
		stage('Checkout SCM') {
			steps {
				git branch:'master', url:'https://github.com/2003280/Vulnerable-Web-Application.git'
			}
		}

		stage('Code Quality Check via SonarQube') {
			steps {
				script{
					def scannerHome = tool 'SonarQube';
					withSonarQubeEnv('SonarQube'){
					sh "${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=OWASP -Dsonar.sources=."}
				}
			}
		}
	}	
	post {
		always{
			recordIssues enabledForFailure: true, tool: sonarQube()
		}
	}
}