pipeline {

  agent any
  triggers {
      cron('*/2 * * * *')
      pollSCM 'H/10 * * * *'
  }
  options {

    buildDiscarder logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '5', daysToKeepStr: '', numToKeepStr: '5')

  }

  stages {

    stage('Hello') {

      steps {
        
        echo "Hello, I'm Cateto Multibranch with prova 2"

      }

    }

  }

}
