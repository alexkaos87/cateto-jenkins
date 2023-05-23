pipeline {

  agent any
  triggers {
      pollSCM 'H/3 * * * *'
  }
  options {

    buildDiscarder logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '5', daysToKeepStr: '', numToKeepStr: '5')

  }

  stages {
    stage('Collect Data') {
      
      steps {
        echo 'clean before any checkout'
        cleanWs()
        echo 'update workspace with latest git repository in default branch master'
        git 'https://github.com/alexkaos87/BankOCR.git'
            }
    stage('Hello') {

      steps {
        
        echo "Hello, I'm Cateto Multibranch with push example on BankOCR"

      }

    }

  }

}
