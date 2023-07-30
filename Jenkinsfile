pipeline {
	agent any
	stages {		
		
		stage ("CI Project"){
			steps {
				bat 'mvn clean install'
			}
			post {
				success {
					archiveArtifacts artifacts : '**/*.war'
				}
			}
		}
		stage ("Deploy build in the Dev CD Pipeline"){
			steps{
				build job : 'Dev-CD-Pipeline'
			}
		}
		stage ('Deploy to Production'){
            		steps{
                		timeout (time: 5, unit:'DAYS'){
                    			input message: 'Approve PRODUCTION Deployment?'
                }
                
                build job : 'Prod-Pipeline'
            }

            post{
                success{
                    echo 'Deployment on PRODUCTION is Successful'
                }

                failure{
                    echo 'Deployement Failure on PRODUCTION'
                }
            }
        }
	}
}
