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
          def customImage = docker.build("sssrkbsc/test1234567:latest")
		  docker.withRegistry('https://hub.docker.com', 'testdockercred') {
          customImage.push()
		  
		  }
        }

      }
    }


  }
  
}