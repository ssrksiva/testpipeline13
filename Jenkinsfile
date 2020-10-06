pipeline {
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
          docker.withRegistry('https://hub.docker.com', 'testdockercred') {
            sh "docker push sssrkbsc/test1234567"
          }
        }

      }
    }

  }
}