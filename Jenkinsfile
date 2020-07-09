pipeline {

 parameters {
  choice choices: ['TEST', 'UAT', 'PROD'], description: 'Select the Environment to Deploy ', name: 'DEPLOY_TO'
}
  stages {
    stage('build-parent-pom-master') {
      when {
        branch 'master'
      }
      steps {
         echo 'Build Completed'
      }
    }
   stage('Deploying to TEST') {
      when {
        branch 'master'
        expression { DEPLOY_TO ==  'TEST' }
      }
       steps {
         echo 'Deploy to TEST Completed'
      }
      }}
  options {
    timeout(time: 1, unit: 'HOURS')
  }
  post {
        always {
            echo 'I will always say Hello again!'
            
            emailext body: "${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}\n More info at: ${env.BUILD_URL}",
                recipientProviders: [[$class: 'DevelopersRecipientProvider'], [$class: 'RequesterRecipientProvider']],
                subject: "Jenkins Build ${currentBuild.currentResult}: Job ${env.JOB_NAME}"
            
        }
  }
}
