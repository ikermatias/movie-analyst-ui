#!groovy

node {
  
  step([$class: 'WsCleanup'])

  stage "Checkout Git repo"
    checkout scm
  stage "Run tests"
    sh "whoami"
    sh "docker run -v \$(pwd):/data --rm usemtech/nodejs-mocha npm install"
    sh "docker run -v \$(pwd):/data --rm usemtech/nodejs-mocha npm install chai chai-http"
    sh "docker run -v \$(pwd):/data --rm usemtech/nodejs-mocha npm test"
}
