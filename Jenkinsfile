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
			}
		}
		stage('Test') {
			steps {
				echo 'Testing...'
				sh 'node --version'
			}
		}
		stage('Deploy') {
			steps {
				echo 'Deploying...'
			}
		}
	}
}
