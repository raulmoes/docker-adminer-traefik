pipeline{
  agent { label 'vps-ssh' }

	environment {
		DOCKERHUB_CREDENTIALS=credentials('dockerhub_id')
	}

	stages {
		stage('Build') {

			steps {
				sh 'sudo docker build -t dockeradminer/dockeradminer:latest .'
			}
		}

		stage('Login') {
			steps {
				sh 'echo $DOCKERHUB_CREDENTIALS_PSW | sudo docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
			}
		}

		stage('Push') {
			steps {
				sh 'sudo docker push dockeradminer/dockeradminer:latest'
			}
		}
	}

	post {
		always {
			sh 'sudo docker logout'
		}
	}

}
