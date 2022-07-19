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
		stage('Remove Unused docker image') {
      		steps{
         		sh "docker rmi $imagename:latest"
			}
    		}
	
	}

	post {
		always {
			sh 'docker logout'
		}
	}
}
