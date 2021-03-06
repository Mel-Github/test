podTemplate(label: 'mypod', serviceAccount: 'jenkins', containers: [ 
    containerTemplate(
      name: 'docker', 
      image: 'docker:19.03.1', 
      command: 'cat', 
      resourceRequestCpu: '100m',
      resourceLimitCpu: '300m',
      resourceRequestMemory: '300Mi',
      resourceLimitMemory: '500Mi',
      ttyEnabled: true,
    )
  ],
            
  volumes: [
    hostPathVolume(mountPath: '/var/run/docker.sock', hostPath: '/var/run/docker.sock'),
  ]
  ) {
    node('mypod') {
        stage('Get latest version of code') {
          checkout scm
        }
        stage('Performing Docker Check') {
            container('docker') {  
                sh 'docker version'   
                sh 'pwd'
                sh 'ls -l'
                sh 'ls -lh ${WORKSPACE}/test.sh'
                sh 'cat ${WORKSPACE}/test.sh'
                //sh 'sleep 4000'
               // sh "${WORKSPACE}/test.sh"
                script {
                    sh '${WORKSPACE}/test.sh'
                }
            }
        }
        stage('Build container') {
            container('docker') {  
                sh 'echo Building Container ${BUILD_ID}'   
                sh 'docker build -t mkdocs:${BUILD_ID} .'
                sh 'docker images'
            }
        }    
        stage('Test container') {
            container('docker') {  
                sh 'cat wrapper.sh'
                sh 'test.sh'
                sh './test.sh'
                sh """
                ./wrapper.sh -v mkdocs-${BUILD_ID} -i mkdocs:${BUILD_ID} -c build -p 8000
                """
            }
        }  
    }
}
