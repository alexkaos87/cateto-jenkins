pipeline {

  agent any
  triggers {
      pollSCM 'H/3 * * * *'
  }
  
  stages {
  
    stage('Hello') {

      steps {
        
        echo "Hello, I'm Cateto Multibranch with push example on BankOCR"

      }

    }
    stage('Collect Data') {
            steps {
                echo 'clean before any checkout'
                cleanWs()
                echo 'update workspace with latest git repository in default branch master'
                git 'https://github.com/alexkaos87/BankOCR.git'
            }
        }

  }

}
