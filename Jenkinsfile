pipeline {
  
  agent any
  
  stages {
    stage('artfacotry') {
      steps {
        ansiColor('xterm') { sh 'ls   -l ' }
        rtDownload (
          serverId: "art",
          spec:
          """{
            "files": [
            {
             "pattern": "example-repo-local/*.war",
              "target": "dist/"
            }
            ]
          }""" )
        
      }
    }
    
    stage('deploy to aws tomcat ') {
      steps {
        
        ansiColor('xterm') { 
          
          sh 'ls dist  -l ' 
          
          withCredentials(bindings: [sshUserPrivateKey(credentialsId: 'aws', keyFileVariable: 'aws')]) {
            sh '''
              scp -o StrictHostKeyChecking=no -o UserKnownHostsFile=/dev/null -i $aws dist/hello-world-war-1.0.0.war ubuntu@172.31.89.50:/var/lib/tomcat7/webapps
              scp -o StrictHostKeyChecking=no -o UserKnownHostsFile=/dev/null -i $aws dist/hello-world-war-1.0.0.war ubuntu@172.31.84.38:/var/lib/tomcat7/webapps
            '''
         }
        }
      }
    }
  }
  
  post {
    always {
      deleteDir()
    }
  }
  
} 
