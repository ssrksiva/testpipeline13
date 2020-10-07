pipeline {
  
  def DOCKER_HOME = tool 'docker'
  env.PATH="${DOCKER_HOME}:${env.PATH}"
  agent any
  stages {
    stage('Pull') {
      steps {
        git(url: 'https://github.com/ssrksiva/testpipeline13.git', branch: 'main', poll: true)
      }
    }

    stage('Check Java') {
      steps {
        sh 'java -version'
      }
    }

    stage('Clean') {
      steps {
        sh 'chmod +x mvnw'
        sh './mvnw -ntp clean -P-webpack'
      }
    }

    stage('Build Image') {
      steps {
        script {
		 sh "./mvnw package -Pprod jib:dockerBuild -Dimage=sssrkbsc/test1234567"
          docker.withRegistry('https://index.docker.io/v1/', 'testdockercred') {
            sh "docker push sssrkbsc/test1234567"
          }
          sh "docker-compose -f src/main/docker/app.yml up"
        }

      }
    }

  }
}