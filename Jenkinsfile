//SCRIPTED
//DECLARATIVE

pipeline {
	 agent any
	// agent { docker { image 'node:13.8' } }
	stages {
		stage('Build') {
			steps {
				echo "Build Nodejs Version"
				// sh 'node --version'
				echo "Print some envioonment Variables...."
				echo "PATH: $PATH"
				echo "BUILD_NUMBER: $env.BUILD_NUMBER"
				echo "BUILD_ID: $env.BUILD_ID"
				echo "BUILD_URL: $env.BUILD_URL"
				echo "BUILD_TAB: $env.BUILD_TAG"
				echo "CHANGE_ID: $env.CHANGE_ID"
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
