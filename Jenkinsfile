pipeline {
  agent any
  stages {
    stage('Pull') {
      steps {
        git(url: 'https://github.com/ssrksiva/testpipeline9.git', branch: 'master', poll: true)
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

    stage('install tools') {
      steps {
        sh './mvnw -ntp com.github.eirslett:frontend-maven-plugin:install-node-and-npm -DnodeVersion=v10.16.0 -DnpmVersion=6.9.0'
      }
    }

    stage('npm install') {
      steps {
        sh './mvnw -ntp com.github.eirslett:frontend-maven-plugin:npm'
      }
    }

    stage('backend test') {
      steps {
        sh './mvnw -ntp verify -P-webpack'
      }
    }

    stage('front end') {
      steps {
        sh './mvnw -ntp com.github.eirslett:frontend-maven-plugin:npm -Dfrontend.npm.arguments=\'run test\''
      }
    }

    stage('packaging') {
      steps {
        sh './mvnw -ntp verify -P-webpack -Pprod -DskipTests'
        archiveArtifacts(fingerprint: true, artifacts: '**/target/*.war')
      }
    }

    stage('Sonar') {
      steps {
        withSonarQubeEnv('My SonarQube Server') {
          sh './mvnw -ntp sonar:sonar'
        }

      }
    }
	 def dockerImage
    stage('publish docker') {
        // A pre-requisite to this step is to setup authentication to the docker registry
        // https://github.com/GoogleContainerTools/jib/tree/master/jib-maven-plugin#authentication-methods
        sh "./mvnw package -Pprod jib:dockerBuild"
		docker.withRegistry('https://hub.docker.com/', 'testdockercred') {
        dockerImage.push()
        customImage = docker.build("sssrkbsc/test12345:latest")

        /* Push the container to the custom Registry */
        customImage.push()
		
    }
    }
}
    
}