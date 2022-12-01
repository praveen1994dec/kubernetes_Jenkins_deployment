pipeline{

	agent any

	environment {
		DOCKERHUB_CREDENTIALS=credentials('dockerhubcred')
	}

	stages {

		stage('Build') {

			steps {
				sh 'docker build -t praveensingam1994/nodeapp:latest .'
			}
		}

		stage('Login') {

			steps {
				sh 'echo $DOCKERHUB_CREDENTIALS | docker login -u "praveensingam1994" --password-stdin'
			}
		}

		stage('Push') {

			steps {
				sh 'docker push praveensingam1994/nodeapp:latest'
			}
		}
	}

	post {
		always {
			sh 'docker logout'
		}
	}

}
