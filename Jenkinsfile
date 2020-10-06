pipeline {
  agent any
  stages {
    stage('Pull') {
      steps {
        git(url: 'https://github.com/ssrksiva/testpipeline9.git', branch: 'master', poll: true)
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