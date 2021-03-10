def FAILED_STAGE
def allJob = env.JOB_NAME.tokenize('/') as String[];
def projectName = allJob[0];
pipeline {
	agent any
	stages {
		stage('Build') {
			steps {
				script {
					FAILED_STAGE=env.STAGE_NAME
					echo "Testing ${env.STAGE_NAME}"
				}
			}
		}
		stage('Test'){
			steps {
				script {
					FAILED_STAGE=env.STAGE_NAME
					echo "Testing ${env.STAGE_NAME}"
					exit 1
				}
			}
		}
		stage('Deploy') {
			steps {
				script {
					FAILED_STAGE=env.STAGE_NAME
					echo "Testing ${env.STAGE_NAME}"
				}
			}
		}
	}
	post {
		failure {
			script {
				mail to: 'sd.gcp.ae@gmail.com',
				cc: '',
            			subject: "Failed Pipeline: ${currentBuild.fullDisplayName}",
             			body: "Something is wrong with the ${projectName}-${env.GIT_BRANCH}-Branch-Build-${env.BUILD_NUMBER} Pipeline in the ${FAILED_STAGE} stage.\nBuild URL: ${env.BUILD_URL}"
			}
		}
		success {
			echo 'I am sending a notification with success'
		}
	}
}
