pipeline{

	agent any

	environment {
		imagename = "rinshad11/nodeapp"
		registryCredential = 'rinshad11'
	}

	stages {
		
		stage('Cloning Git') {
      			steps {
        		git([url: 'https://github.com/rinshad1/custom-nodejsapp.git', branch: 'main'])
 
     				   }
   			   }
		
		

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
