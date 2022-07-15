pipeline{

	agent any

	environment {
		imagename = "kevalnagda/flaskapp"
		DOCKERHUB_CREDENTIALS=credentials('dockerhub-cred-raja')
	}

	stages {

		stage('Building image') {
                           steps{
                           script {
                                dockerImage = docker.build imagename
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
