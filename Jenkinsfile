pipeline {
    agent any
    tools {
      nodejs "NodeJs"
    }
    stages {
    	stage('verify') {
			steps{
				sh 'node -v'
			}
		}
        stage('build') {
            steps {
                sh 'npm install'
                sh 'npm run build'
            }
        }
        stage('deploy') {
            when {
                branch 'master'
            }
            steps {
                sh 'ng deploy'
            }
        }
    }
    post {
        success {
            script {
                if ("${env.BRANCH_NAME}" == 'master')
                    slackSend channel: 'jenkins-training', color: 'good', 
                        message: 'Success ${env.JOB_NAME} ${currentBuild.DisplayName} ${currentBuild.absoluteUrl} from Souleymane', 
                        tokenCredentialId: 'slack-token-bon', teamDomain: 'devinstitut'
						
					discordSend description: "Success ${currentBuild.displayName} ${currentBuild.absoluteUrl}", 
                        footer: "Souleymane a réussi commit: ${env.GIT_COMMIT}", image: '', link: '', result: 'SUCCESS', thumbnail: '',
                        title: "${env.JOB_NAME}", 
                        webhookURL: 'https://discordapp.com/api/webhooks/747819422705778738/dHWPHidlNLpiiKftWU84__Ss2LAkws77Swfdk5OWs22qla3hlI1B4zywW8ROg4nAwjRM'
                    
            }
        }
        failure {
            slackSend channel: 'jenkins-training', color: 'danger', 
                 message: 'Failure ${env.JOB_NAME} ${currentBuild.displayName} ${currentBuild.absoluteUrl} from Souleymane',
                tokenCredentialId: 'slack-token-bon', teamDomain: 'devinstitut'
				
			discordSend description: "Failure ${currentBuild.displayName} ${currentBuild.absoluteUrl}", 
                footer: "Souleymane a échoué commit: ${env.GIT_COMMIT}", image: '', link: '', result: 'FAILURE', thumbnail: '',
               title: "${env.JOB_NAME}", 
                 webhookURL: 'https://discordapp.com/api/webhooks/747819422705778738/dHWPHidlNLpiiKftWU84__Ss2LAkws77Swfdk5OWs22qla3hlI1B4zywW8ROg4nAwjRM'
             
        }
    }
}