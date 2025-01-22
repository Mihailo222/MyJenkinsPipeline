pipeline {

agent {
 label 'agent1'
}

 stages {
  stage('Whoami'){
    script {
      echo "Stage: ${env.STAGE_NAME}"
    }
    sh 'whoami'
  }

   
 } 

}
