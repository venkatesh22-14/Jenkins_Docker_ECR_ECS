pipeline{

	agent any

	environment {
		DOCKERHUB_CREDENTIALS=credentials('docker-cred')
	}

	stages {

		stage('checkout') {
		   
			steps {
			    git branch: 'main', url: 'https://github.com/venkatesh22-14/Jenkins_Docker_ECR_ECS.git'
			
			}
		}

		stage('Docker Build and Tag') {

			steps {
				sh 'docker build -t hexashop .'
                sh 'docker tag hexashop 221488/hexashopwebsite:latest'
			}
		}

		stage('Publish image to Docker Hub') {

			steps {
				withDockerRegistry([ credentialsId: "docker-cred", url: "" ]) {
                sh  'docker push 221488/hexashopwebsite:latest'}
		   }
	   }

	 stage('Run Docker container on Jenkins Agent') {

            steps{
                sh "docker run -d -p 80:80 221488/hexashopwebsite"
            }
        }
    }
 }

