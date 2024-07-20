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
				sh "echo Begin OWASP DependencyCheck"
				dependencyCheck additionalArguments: '--format HTML --format XML', odcInstallation: 'Default'
				sh "echo End OWASP DependencyCheck"
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