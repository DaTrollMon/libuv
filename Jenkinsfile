pipeline {
	agent {
		docker {
			image 'node:8-alpine'
		}
	}

	stages {
		stage('build') {
			steps {
				echo 'Building...'
				slackSend "Build started - ${env.JOB_NAME} ${env.BUILD_NUMBER} (<${env.BUILD_URL}|Open>)"
			}
		}
		stage('Test') {
			steps {
				echo 'Testing...'
				sh 'node --version'
				slackSend "Tests started - ${env.JOB_NAME} ${env.BUILD_NUMBER} (<${env.BUILD_URL}|Open>)" 
			}
		}
		stage('Deploy') {
			steps {
				echo 'Deploying...'
			}
		}
	}
}
