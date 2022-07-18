pipeline{

	environment {
		DOCKERHUB_CREDENTIALS=credentials('dockerhub-cred-raja')
	}
	agent any
	stages {

		stage('Build') {

			steps {
				sh 'docker build -t rinshad11/nodeapp:latest .'
			}
		}

		
		  stage('Scan image') {
    		  anchore engineCredentialsId: 'fbc64e9a-9d15-4c52-9ad4-23535aa2af2e', engineurl: 'ec2-52-91-231-102.compute-1.amazonaws.com:8228/v1', name: 'anchore_images'
  			}
		
	
		stage('Login') {

			steps {
				sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
			}
		}

		stage('Push') {

			steps {
				sh 'docker push rinshad11/nodeapp:latest'
			}
		}
	}

	post {
		always {
			sh 'docker logout'
		}
	}

}
