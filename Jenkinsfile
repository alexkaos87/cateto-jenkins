pipeline {

  agent any
  triggers {
      cron('*/5 * * * *')
      pollSCM 'H/2 * * * *'
  }
  options {

    buildDiscarder logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '5', daysToKeepStr: '', numToKeepStr: '5')

  }

  stages {

    stage('Hello') {

      steps {
        
        echo "Hello, I'm Cateto Multibranch"

      }

    }

  }

}
