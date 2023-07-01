pipeline{

	agent any

	environment {
		DOCKERHUB_CREDENTIALS=credentials('docker-cred')
	}

	stages {

		stage('checkout') {
		   
			steps {
			    git branch: 'master', url: 'https://github.com/venkatesh22-14/Jenkins_Docker_ECR.git'
			
			}
		}

		stage('Docker Build and Tag') {

			steps {
				sh 'docker build -t latest .'
                sh 'docker tag yogast 221488/yogastwebsite:latest'
			}
		}

		stage('Publish image to Docker Hub') {

			steps {
				withDockerRegistry([ credentialsId: "docker-cred", url: "" ]) {
                sh  'docker push 221488/yogastwebsite:latest'}
		   }
	   }

	 stage('Run Docker container on Jenkins Agent') {

            steps{
                sh "docker run -d -p 8003:8080 221488/yogastwebsite"
            }
        }
    }
 }

