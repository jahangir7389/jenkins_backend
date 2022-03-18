pipeline {
  agent any
  environment {
		registryCredential = 'dockerhub' 
	}
  stages {
    stage('Build') {
			steps {
				dir('.'){
					sh 'docker build -t jahangir7389/jenkins-backend-app .'
				}
			} 
		}
    stage('Test') {
      steps {
			dir('.'){
				sh 'docker container run --rm -p 8002:8080 --name python -d jahangir7389/jenkins-backend-app ' 
				sh 'sleep 5'
				sh 'curl -I http://localhost:8001'
			}
		} 
	}
    stage('Publish') {
			steps{
				script {
					docker.withRegistry( '', registryCredential ) {
						sh 'docker push jahangir7389/jenkins-backend-app:latest'
					} 
				}
			} 
		}
	}
}
