pipeline {

agent any

 stages {
  stage('Whoami'){
    script {
      echo "Stage: ${env.STAGE_NAME}"
    }
    sh 'whoami'
  }

   
 } 

}
