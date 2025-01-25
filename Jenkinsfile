pipeline {
    agent {label 'agent1'}

    stages {
 //       stage('Checkout') { //nece da radi bez checkout-a; multibranch pipeline
 //           steps {
 //               checkout([$class: 'GitSCM', 
 //                         branches: [[name: '*/main']],
 //                         userRemoteConfigs: [[url: 'https://github.com/Mihailo222/MyJenkinsPipeline.git']]])
//            }
  //      }

        stage('Whoami') {
            steps {
                echo "Stage: ${env.STAGE_NAME}"
                sh 'whoami'
            }
        }
    }
}


