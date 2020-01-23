pipeline {
    agent none
    options {
        buildDiscarder(logRotator(numToKeepStr: '20')) 
    }
    parameters {
        choice(
            choices: ['Ubuntu Bionic' , 'Ubuntu Xenial'],
            description: '',
            name: 'REQUESTED_BUILD'
        )
//        gitParameter name: 'TAG', type: 'PT_TAG', defaultValue: 'latest'
//        gitParameter branchFilter: 'origin/(.*)', defaultValue: 'master', name: 'BRANCH', type: 'PT_BRANCH'
    }
   stages {
      stage('Build Ubuntu Bionic') {
         when {
                expression { params.REQUESTED_BUILD == 'Ubuntu Bionic' }
            }
         agent {
            node { label 'bionic && nfs' } 
         }
         steps {
            // Get some code from a GitHub repository
            //git branch: "refs/tags/${params.TAG}", url: "${GIT_URL}" //, url: 'https://github.com/emetriq/efs-utils'

            // Run Maven on a Unix agent.
            sh "./build-deb.sh"

         }

         post {
            success {
               archiveArtifacts 'build/amazon-efs-utils*deb'
            }
         }
      }
   }
}
