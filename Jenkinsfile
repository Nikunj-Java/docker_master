def containerName="dokcer_container"
def imageName="dokcer_master"
def tag="latest"
 
node {
	 
    
  stage('Checkout Source Code') {
    checkout scm
  }
 
    stage('Image Build'){
        sh "docker build -t $imageName:${env.BUILD_NUMBER} --pull --no-cache ."
        echo "Image build complete"
    }
   
    stage ('Run Application') {
    try {
      // Stop existing Container
      // sh 'docker rm $containerName -f'
      // Start database container here
      sh "docker run -d --name $containerName-${env.BUILD_NUMBER} -p 80:80 $imageName:${env.BUILD_NUMBER}"
       

    } 
	catch (error) {
    } finally {
      // Stop and remove database container here
      echo "error occured"
    }
 
  }

 	
 
}
