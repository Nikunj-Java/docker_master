node {
 
  stage('Checkout Source Code') {
    checkout scm
  }

  stage('Create Docker Image') {
    docker.build("sudo docker_image:${env.BUILD_NUMBER}")
  }

  stage ('Run Application') {
    try {
      // Stop existing Container
      sh 'sudo docker rm docker_container -f'
      // Start database container here
      sh "sudo docker run -d --name docker_container docker_image:${env.BUILD_NUMBER}"
	    //push to docker hub
	    
	//sh "sudo docker push nikunj0510/docker_image:${env.BUILD_NUMBER}"
    } 
     
catch (error) {
    } finally {
      // Stop and remove database container here
      
    }
  }
 
  
  
   
 }
