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
    sh "docker run -v \$(pwd):/data --rm usemtech/nodejs-mocha npm install"
    sh "docker run -v \$(pwd):/data --rm usemtech/nodejs-mocha npm install chai chai-http"
    sh "docker run -v \$(pwd):/data --rm usemtech/nodejs-mocha npm test"
  stage "Push image"
    dockerImage = docker.build("ikermatias/movieapp")
    docker.withRegistry('', "dockerhub"){
    dockerImage.push("latest")
    }

  stage "Trigger downstream" 
    build job: "movie-CD", wait: false

    
}
