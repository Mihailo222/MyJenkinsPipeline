//pipeline variables
deleteWorkspace=false


pipeline {
    agent {label 'agent1'}
    environment {
        //ARTIFACTORY_CREDENTIALS = "${CONSTANTS.ServiceAccountUser}"
        CLOUD_VM_IP="10.0.1.6"
        DOCKERHUB_FAILING_SA="failing_sa"
        DOCKERHUB_SA="dockerhub-svc-account"
        CLOUD_CONF_VM_CREDS="ansible_deployed_cloud_vm"
        
    }

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
        
        stage('Connect to cloud VM via SSH'){
            steps{

            echo "Stage: ${env.STAGE_NAME}"
            withCredentials([sshUserPrivateKey(credentialsId: 'ansible_deployed_cloud_vm', keyFileVariable: 'MY_SSH_KEY', usernameVariable: 'MY_SSH_USERNAME')]) //custom name for keyFileVariable for referencing later in the pipeline
            {
                sh '''
                    ssh -i $MY_SSH_KEY ${MY_SSH_USERNAME}@${CLOUD_VM_IP} "ls -la"
                '''
            }
            }
       }

        
        stage('Check docker version installed on cloud deployable VM'){
            steps{

            echo "Stage: ${env.STAGE_NAME}"
            withCredentials([sshUserPrivateKey(credentialsId: 'ansible_deployed_cloud_vm', keyFileVariable: 'MY_SSH_KEY', usernameVariable: 'MY_SSH_USERNAME')]) //custom name for keyFileVariable for referencing later in the pipeline
            {
                sh '''
                    ssh -i $MY_SSH_KEY ${MY_SSH_USERNAME}@${CLOUD_VM_IP} "docker -v"
                '''
            }
            }
       }

    stage('Login to Docker Hub via service account from cloud configurable VM'){

    steps {
        withCredentials([
            usernamePassword(credentialsId: 'dockerhub-svc-account', usernameVariable: 'SVCUSERNAME', passwordVariable: 'SVCPASSWD')        
        ])
        { //get username and password from usernamePassword Jenkins global credential representing service account that stores credentials for dockerhub
         withCredentials([
             sshUserPrivateKey(credentialsId: 'ansible_deployed_cloud_vm', keyFileVariable: 'MY_SSH_KEY', usernameVariable: 'MY_SSH_USERNAME')
         ]){
            
            sh '''
                    ssh -i $MY_SSH_KEY ${MY_SSH_USERNAME}@${CLOUD_VM_IP} "docker login --username ${SVCUSERNAME} --password ${SVCPASSWD}"
                '''
         }   
        }
    }
    }

    stage('Check DockerHub credentials ') {
        steps {
        withCredentials([
            usernamePassword(credentialsId: 'dockerhub-svc-account', usernameVariable: 'SVCUSERNAME', passwordVariable: 'SVCPASSWD')        
        ])
        { //get username and password from usernamePassword Jenkins global credential representing service account that stores credentials for dockerhub
         withCredentials([
             sshUserPrivateKey(credentialsId: 'ansible_deployed_cloud_vm', keyFileVariable: 'MY_SSH_KEY', usernameVariable: 'MY_SSH_USERNAME')
         ]){
            
           /* sh '''
                    ssh -i $MY_SSH_KEY ${MY_SSH_USERNAME}@${CLOUD_VM_IP} "docker login --username ${SVCUSERNAME} --password ${SVCPASSWD}"
                '''*/
            script {

                String SA_user="${SVCUSERNAME}"
                String SA_pass="${SVCPASSWD}"
                String credentialsId="${credentialsID}"
                checkServiceAccount(credentialsId, SA_user, SA_pass)
            }

         }   
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


def checkServiceAccount(String credentialsId, String username, String password){
//prima credential iz COMMON-a

}


