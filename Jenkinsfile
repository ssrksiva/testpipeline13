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
            sh 'docker push ${DOCKER_IMAGE_TAG}'
          }
        }

      }
    }

  }
  environment {
    DOCKER_IMAGE_TAG = sssrkbsc/test1234567
  }
}