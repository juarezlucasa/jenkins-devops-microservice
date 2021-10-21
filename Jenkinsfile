//SCRIPTED
//DECLARATIVE

pipeline {
	 agent any
	// agent { docker { image 'node:13.8' } }
	environment {
		dockerHome = tool 'MyDocker'
		mavenHome = tool 'MyMaven'
		PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
	}

	stages {
		stage('Checkout') {   //Lo hace implicito jenkins por pipeline, pero por las dudas lo declaramos
			steps {
				echo "Build First Microservice in javascript"
				sh 'mvn --version'
				sh 'docker version'
				echo "Prints envionment Variables...."
				echo "PATH: $PATH"
				echo "BUILD_NUMBER: $env.BUILD_NUMBER"
				echo "BUILD_ID: $env.BUILD_ID"
				echo "BUILD_URL: $env.BUILD_URL"
				echo "BUILD_TAB: $env.BUILD_TAG"
				echo "CHANGE_ID: $env.CHANGE_ID"
			}	
		}

		stage('Build - Compile') {
			steps {
				echo "Arranco a compilar la app"
				sh "mvn clean compile"
			}	
		}

		stage('Test') {
			steps {
				echo "Comienzo test unitarios"
				sh "mvn test"
			}	
		}	

		stage('Integration Test') {
			steps {
				echo "Comienzo test de integración"
				sh "mvn failsafe:integration-test failsafe:verify"
			}	
		}

		stage('Package JAR File') {
			steps {
				echo "Comienzo a generar el jar"
				sh "mvn package -DskipTests"
			}	
		}		

		stage('Build Docker Image') {
			steps {
				echo "Comienzo a buildear la imagen"
				script {
					dockerImage = docker.build("juarezlucavs/currecy-exchange-devops:${env.BUILD_TAG}")
				}
			}	
		}

		stage('Push Docker Image') {
			steps {
				echo "Comienzo a buildear la imagen"
				script {
					docker.withRegistry('','dockerhub') {
						dockerImage.push();
						dockerImage.push('latest');
					} 
				}
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
