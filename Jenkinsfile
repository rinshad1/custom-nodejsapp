pipeline{

	agent any

	environment {
		imagename = "rinshad11/nodeapp"
		registryCredential = 'dockerhub-cred-raja'
	}

	stages {

		stage('Building image') {
                           steps{
				   script {
					   dockerImage = docker.build ${env.imagename}
                                   }
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
	}

	post {
		always {
			sh 'docker logout'
		}
	}

}
