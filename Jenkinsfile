pipeline {
	agent any
	environment {
		DOCKERHUB_CREDENTIALS=credentials('dockerhub')
	}
	stages {
		stage('Build') {
			steps {
				echo 'BUILDING SOFTWARE'
				sh 'docker-compose build --no-cache'
				sh 'docker-compose up --force-recreate --exit-code-from build-agent build-agent'
			}
			post {
				failure {
					echo 'ERROR IN BUILDING'
					sh 'false'
				}
				success {
					echo 'SUCCESS IN BUILDING'
				}
			}
		}
		stage('Test') {
			steps {
                		echo 'Testing'
                		sh 'docker-compose build --no-cache'
				sh 'docker-compose up --force-recreate --exit-code-from test-agent test-agent'
			}
			post {
				failure {
					echo 'ERROR IN TESTING'
					sh 'false'
				}
				success {
					echo 'SUCCESS IN TESTING'
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
				sh 'docker push arturhamerski98/build-agent:latest'
			}
			post {
				failure {
					echo 'ERROR IN PUSHING'
					sh 'false'
				}
				success {
					echo 'SUCCESS IN PUSHING'
				}
			}
			
		}
		
		
	}
}
