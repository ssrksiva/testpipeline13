pipeline {
  agent any
  stages {
    stage('Pull') {
      steps {
        git(url: 'https://github.com/ssrksiva/testpipeline13.git', branch: 'main', poll: true)
      }
    }

    
	 
    stage('publish docker') {
        // A pre-requisite to this step is to setup authentication to the docker registry
        // https://github.com/GoogleContainerTools/jib/tree/master/jib-maven-plugin#authentication-methods
		steps {
        
		
        
        def customImage = docker.build("sssrkbsc/test12345:latest")

        /* Push the container to the custom Registry */
        customImage.push()
		
		
    }
    }
}
    
}