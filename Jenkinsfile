//pipeline variables
deleteWorkspace=false


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
        stage('Login to cloud VM via SSH'){
            steps{

            echo "Stage: ${env.STAGE_NAME}"
            withCredentials([sshUserPrivateKey(credentialsId: 'ansible_deployed_cloud_vm', keyFileVariable: 'MY_SSH_KEY')])
            {
                sh '''
                    ssh -i $MY_SSH_KEY myawesomeprojectwideuser@40.85.177.80 "whoami"
                '''
            }
            }
       }
    }
    post {
        always {
            echo "Build finished."
            echo "This is the workspace build happened in: ${env.WORKSPACE}"
            script {
                dir("${env.WORKSPACE}@tmp"){ // pipelineScreenName_branch@tmp
                    deleteDir()
                }
                if(deleteWorkspace == true){
                    echo "Cleaning workspace..."
                    dir("${env.WORKSPACE}"){  // pipelineScreenName_branchName
                        deleteDir()
                    }
                }
            } 
        }
    }
    
}


