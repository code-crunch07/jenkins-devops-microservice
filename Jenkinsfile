//scriped
// DECLARATIVE

pipeline {
	agent any
	// agent { docker { image 'maven:3.9.9'} }
	// agent { docker { image 'node:23.11.0'} }
	environment {
		dockerHome = tool 'myDocker'
		mavenHome = tool 'myMaven'
		PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
	}

	stages {
		stage('Checkout'){
			steps {
				sh 'mvn --version'
				sh 'docker --version'
				echo "Build"
				echo "PATH - $PATH"
				echo "BUILD_NUMBER - $env.BUILD_NUMBER"
				echo "BUILD_ID - $env.BUILD_ID"
				echo "JOB_NAME - $env.JOB_NAME"
				echo "BUILD_TAG - $env.BUILD_TAG"
				echo "BUILD_URL - $env.BUILD_URL"
			}
		}

		stage ('Build') {
			steps {
				sh "mvn clean compile"
			}
		}

		stage('Test'){
			steps {
				sh "mvn test"
			}
		}

		stage('Integration Test'){
			steps {
				sh "mvn failsafe:integration-test failsafe:verify"
			}
		}

		stage ('Package') {
			steps {
				sh "mvn package -DskipTests"
			}
		}

		stage ('Build Docker image') {
			steps {
				// "docker build -t /codecrunchweb/currency-exchange-devops/:$env.BUILD_TAG"
				script {
					dockerImage = docker.build("/codecrunchweb/currency-exchange-devops/:${env.BUILD_TAG}")
				}

			}
		}

		stage ('Pudh Docker Image') {
			steps {
				script {
					docker.withRegistery('', 'dockerhubid') {
						dockerImage.push();
						dockerImage.push('latest');
					}
				}
			
			}
		}	
	} 

	post {
		always {
			echo 'Im awesome. I run always'
		}
		
		success {
			echo 'im run whenyou are successfull'
		}

		failure {
			echo 'i run when you fail'
		}
	}
}