//SCRIPTED
//DECLARATIVE

pipeline {
	// agent any
	agent { docker { image 'node:13.8' } }
	stages {
		stage('Build') {
			steps {
				echo "Build Nodejs Version"
				sh 'node --version'
			}	
		}
		stage('Test') {
			steps {
				echo "Test"
			}	
		}
		stage('Integration Test') {
			steps {
				echo "Integration Test"
			}	
		}		
	}

	post{
		always {
			echo "I run always"
		}
		success {
			echo "I run when you're successful"
		}		
		failure {
			echo "I run when you fail"
		}		
	}
}
