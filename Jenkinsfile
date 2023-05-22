pipeline {

  agent any
  triggers {
      cron('*/3 * * * *')
  }
  options {

    buildDiscarder logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '5', daysToKeepStr: '', numToKeepStr: '5')

  }

  stages {

    stage('Hello') {

      steps {
        
        echo "hello, i'm multibranch job"

      }

    }

  }

}
