pipeline {
	agent any

	stages {
		stage('Build') {
			steps {
				echo 'Building...'
				dir("${env.WORKSPACE}") {
					sh 'autogen.sh'
					sh 'configure'
					sh 'make'
					sh 'make check'
					sh 'make install'
				}
				slackSend color: "#439FE0", message: "Build started - ${env.JOB_NAME} ${env.BUILD_NUMBER} (<${env.BUILD_URL}|Open>)"
			}
		}
		stage('Test') {
			steps {
				echo 'Testing...'
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
