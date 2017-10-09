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
				slackSend color: "#439FE0", message: "Build started - ${env.JOB_NAME} ${env.BUILD_NUMBER} (<${env.BUILD_URL}|Open>)"
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
	post {
		always {
			echo 'Cleanup'
			deleteDir()
		}
		success {
			echo 'I succeeded'
      slackSend color: 'good',
                message: "The pipeline ${currentBuild.fullDisplayName} completed successfully."
    }
		unstable {
			echo "I\'m unstable"
		}
		failure {
			echo 'I failed'
		}
		changed {
			echo 'Things were different before'
		}
	}
}
