//Scriptes Pipeline

// node {
// 	stage('Build') {
// 		echo "Build"
// 	}
// 	stage('Test') {
// 		echo "Test"
// 	}
// 	stage('Integration Test') {
// 		echo "Integration Test"
// 	}
// }

//Declarative pipeline

pipeline {
	agent any
	//agent { docker { image 'maven:3.6.3'}}
    environment{
		dockerHome = tool 'myDocker'
		mavenHome = tool 'myMaven'
		PATH = "$dockerHome/bin:$mavenHome/bin:$PATH "
	}

	stages {
		stage('Checkout') {
			steps {
				echo "Build"
				sh 'mvn --version'
				sh 'docker version'
			}
		}
		stage('Compile') {
			steps {
				echo "Maven Compile"
				sh 'mvn clean compile'
			}
		}

		stage('Test') {
			steps {
				echo "Maven Test"
				sh 'mvn test'
			}
		}
		stage('Integration Test') {
			steps {
				echo "Integration Test"
				sh "mvn failsafe:integration-test failsafe:verify"
			}
		}
	} 
	post {
		always{
			echo "I run always"
		}
		success{
			echo "I run when successfully"
		}
		failure{
			echo'I run when fail'
		}
	}

}