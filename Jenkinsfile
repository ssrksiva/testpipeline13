pipeline {
  agent any
  stages {
    stage('Pull') {
      steps {
        git(url: 'https://github.com/ssrksiva/testpipeline13.git', branch: 'main', poll: true)
      }
    }

    
	 
     stage('Build Image') {
        steps {
           script {
            def image = docker.build("-f Dockerfile.local", "--no-cache", "-t ${DOCKER_IMAGE_TAG}")
           }
        }
    }
	
	  stage('Deploy') {
            steps {
                script {
                    docker.withRegistry('https://hub.docker.com', 'testdockercred') {
                        image.push(${DOCKER_IMAGE_TAG})
                    }
                }
            }
}
}
    
}