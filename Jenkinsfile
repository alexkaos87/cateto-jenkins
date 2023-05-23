pipeline {

  agent any
  triggers {
      cron('*/5 * * * *')
  }
  options {

    buildDiscarder logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '5', daysToKeepStr: '', numToKeepStr: '5')
     overrideIndexTriggers(false)

  }

  stages {

    stage('Hello') {

      steps {
        
        echo "Hello, I'm Cateto Multibranch"

      }

    }

  }

}
