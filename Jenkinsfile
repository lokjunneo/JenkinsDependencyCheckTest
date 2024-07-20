pipeline {
	agent any
	stages {
		stage('Checkout SCM') {
			steps {
				sh "echo Begin stage Checkout SCM"
				git credentialsId: 'lmaoJquery', url: 'https://github.com/lokjunneo/JenkinsDependencyCheckTest.git'
				sh "echo End stage Checkout SCM"
			}
		}

		stage('OWASP DependencyCheck') {
			steps {
				dependencyCheck additionalArguments: '''--format ALL
				--out "./"
				--scan "./"
				--prettyPrint''', nvdCredentialsId: 'NVD_API_Key_1', odcInstallation: 'OWASP Dependency Check'
			}
		}
	}	
	post {
		success {
			sh "echo Report..."
			dependencyCheckPublisher pattern: 'dependency-check-report.xml'
			sh "echo ...report"
		}
	}
}