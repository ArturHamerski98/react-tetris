pipeline {
	agent any
	
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
				sh 'echo Arturekh18! | docker login -u arturhamerski98 --password-stdin'
			}
		}

		stage('Push') {

			steps {
				sh 'docker push arturhamerski98/build-agent:latest'
			}
		}
		
		
	}
}
