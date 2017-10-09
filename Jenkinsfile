pipeline {
	agent any

	stages {
		stage('Build') {
			steps {
				slackSend color: "#439FE0", message: "Build started - ${env.JOB_NAME} ${env.BUILD_NUMBER} (<${env.BUILD_URL}|Open>)"
				echo 'Building...'
				dir("${env.WORKSPACE}") {
					sh './autogen.sh'
					sh './configure'
					sh 'make'
					sh 'make check'
				}
			}
		}
		stage('Test') {
			steps {
				echo 'Testing...'
				slackSend "Tests started - ${env.JOB_NAME} ${env.BUILD_NUMBER} (<${env.BUILD_URL}|Open>)"
				dir("${env.WORKSPACE}") {
					checkout
						changelog: false,
						poll: false,
						scm: [$class: 'GitSCM', branches: [[name: '*/master']],
						doGenerateSubmoduleConfigurations: false,
						extensions: [[$class: 'RelativeTargetDirectory', relativeTargetDir: 'gyp']],
						submoduleCfg: [],
						userRemoteConfigs: [[url: 'https://chromium.googlesource.com/external/gyp.git']]]
					sh './gyp_uv.py -f make'
					sh 'make -C out'
					sh './out/Debug/run-tests'
				}
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
