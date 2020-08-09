#!/usr/bin/env groovy
pipeline { 
  agent { 
    node { 
      label 'docker'
    }
  }
 
  stages {
    stage ('Checkout Code') {
      steps {
        checkout scm
      }
    }
    stage ('Verify Tools'){
      steps {
        parallel (
          docker: { sh "docker -v" }
        )
      }
    }
    stage ('Verify') {
      steps {
        input "Everything good?"
      }
    }

  }
}
