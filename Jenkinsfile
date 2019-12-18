#!groovy

node {

  environment {
    registry = "ikermatias/movieapp"
    registryCredential = 'dockerhub'
  }
  
  step([$class: 'WsCleanup'])

  stage "Checkout Git repo"
    checkout scm
  stage "Run tests"
    sh "whoami"
    sh "docker run -v \$(pwd):/data --rm usemtech/nodejs-mocha npm install"
    sh "docker run -v \$(pwd):/data --rm usemtech/nodejs-mocha npm install chai chai-http"
    sh "docker run -v \$(pwd):/data --rm usemtech/nodejs-mocha npm test"
  stage "Push image"
    dockerImage = docker.build("ikermatias/movieapp")
    docker.withRegistry('', "3567c3dd-1691-499a-9975-2f450e97ad34"){
    dockerImage.push("latest")
    }

    
}
