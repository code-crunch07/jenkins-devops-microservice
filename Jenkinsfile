//scriped
// DECLARATIVE

pipeline{
	// agent any
	agent { docker { image 'maven:3.9.9'} }
	stages {
		stage('Build'){
			steps {
				sh 'mvn --version'
				echo "Build"
			}
		}
		stage('Test'){
			steps {
				echo "Test"
			}
		}
		stage('Integration Test'){
			steps {
				echo "Integration Test"
			}
		}
	} 
	post{
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