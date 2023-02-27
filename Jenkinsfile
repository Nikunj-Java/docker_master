node {
environment {
    DOCKERHUB_CREDENTIALS = credentials('DockerHub crendentials')
  }
  stage('Checkout Source Code') {
    checkout scm
  }

  stage('Create Docker Image') {
    docker.build("docker_image:${env.BUILD_NUMBER}")
  }

  stage ('Run Application') {
    try {
      // Stop existing Container
      sh 'docker rm docker_container -f'
      // Start database container here
      sh "docker run -d --name docker_container docker_image:${env.BUILD_NUMBER}"
	    //push to docker hub
	    
	//sh "docker push nikunj0510/docker_image:${env.BUILD_NUMBER}"
    } 
     
catch (error) {
    } finally {
      // Stop and remove database container here
      
    }
  }
	
 stage('Login') {
      steps {
        sh "echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin"
      }
    }
  stage('Push') {
      steps {
        sh "docker push nikunj0510/docker_image:${env.BUILD_NUMBER}"
      }
    }
   
 }
