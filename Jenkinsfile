pipeline {

  agent any
  triggers {
      cron('*/1 * * * *')
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
