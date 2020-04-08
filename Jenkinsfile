/*  import shared library */
@Library('jenkins-shared-library')_

pipeline {
    agent none
    stages {        
        stage('Check go syntax') {
            agent { docker {
                  image 'cytopia/golint' 
                  args '--entrypoint=' 
                  } }
            steps {
                script { bashCheck }
            }
        }
        stage('Check Dockerfile syntax') {
            agent { docker { image 'hadolint/hadolint' } }
            steps {
                sh 'hadolint --ignore DL3022 --ignore DL3006 \${WORKSPACE}/fake-backend/Dockerfile'
            }
        }   
    }
    post {
        always {
            script {
                /* Use slackNotifier.groovy from shared library and provide current build result as parameter */
                clean
                slackNotifier currentBuild.result
             }
         }
     }
}
