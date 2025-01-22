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

/*
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
}*/

pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout([$class: 'GitSCM', 
                          branches: [[name: '*/main']], // Zameni 'main' imenom grane, ako je drugačije
                          userRemoteConfigs: [[url: 'https://github.com/Mihailo222/MyJenkinsPipeline.git']]])
            }
        }

        stage('Whoami') {
            steps {
                echo "Stage: ${env.STAGE_NAME}"
                sh 'whoami'
            }
        }
    }
}


