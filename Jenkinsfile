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

		
		  node {
 		  def imageLine = 'rinshad11/nodeapp:latest'
  		  writeFile file: 'anchore_images', text: imageLine
  		  anchore name: 'my_image_file', engineCredentialsId: 'ubuntu'
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
