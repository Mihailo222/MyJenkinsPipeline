/*pipeline {

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

}*/


pipeline {
    agent {
        label 'agent1'
    }

    stages {
        stage('Whoami') {
            steps {
                echo "Stage: ${env.STAGE_NAME}"
                sh 'whoami'
            }
        }
    }
}

