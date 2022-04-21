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
  stage('Docker Build') {
            steps {
                echo '----------------- This is a build docker image phase ----------'
                sh '''
                    docker image build -t docker_master .
                '''
            }
        }

   stage('Docker Deploy') {
            steps {
                echo '----------------- This is a docker deploment phase ----------'
                sh '''
                 (if  [ $(docker ps -a | grep docker_master | cut -d " " -f1) ]; then \
                        echo $(docker rm -f docker_master); \
                        echo "---------------- successfully removed docker_master ----------------"
                     else \
                    echo OK; \
                 fi;);
            docker container run --restart always --name docker_master -p 8081:8081 -d docker_master
            '''
            }
    }
  
   
 }
