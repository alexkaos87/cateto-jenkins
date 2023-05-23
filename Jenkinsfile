pipeline {

  agent any
  triggers {
      pollSCM 'H/3 * * * *'
  }
  options {

    buildDiscarder logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '5', daysToKeepStr: '', numToKeepStr: '5')

  }

  stages {

    stage('Hello') {

      steps {
        
        echo "Hello, I'm Cateto Multibranch with push example on BankOCR"

      }

    }

  }

}
