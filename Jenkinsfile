pipeline {
  agent any
  stages {
    stage('Script') {
      steps {
        container('build') { 
          sh './test.sh'
          docker version
        }
      }
    }

  }
}
