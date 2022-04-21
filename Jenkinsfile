node {
  
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
    } 
	catch (error) {
    } finally {
      // Stop and remove database container here
      
    }
  }
	
 stage('Docker Deploy') {
            steps {
                echo '----------------- This is a docker deploment phase ----------'
                sh '''
                 (if  [ $(docker ps -a | grep ecom-webservice | cut -d " " -f1) ]; then \
                        echo $(docker rm -f ecom-webservice); \
                        echo "---------------- successfully removed ecom-webservice ----------------"
                     else \
                    echo OK; \
                 fi;);
            docker container run --restart always --name ecom-webservice -p 8081:8081 -d ecom-webservice
            '''
            }
  }
   
  
   
 }
