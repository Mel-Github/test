pipeline {
  agent any
  stages {
    stage('Script') {
      steps {
        container(name: 'build') {
          sh './test.sh'
          sh 'docker version'
        }

      }
    }

  }
}