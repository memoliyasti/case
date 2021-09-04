pipeline {
  agent any
  triggers {
      pollSCM '* * * * *'
  }
  stages {
      stage('Build') {
          steps {
              sh './mvn clean install'
          }
      }
      stage('Test') {
          steps {
              sh './mvn src/test'
          }
      }

    stage('docker build/push') {
      docker.withRegistry('https://index.docker.io/v1/', 'dockerhub') {
        def app = docker.build("memoliyasti/docker-springboot-demo:${commit_id}", '.').push()
     }
   }
}
