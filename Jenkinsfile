pipeline {
    agent any
    triggers {
      cron('*/3 * * * *') // # at the 0.00 of every Sunday H 0 * * 0
      pollSCM 'H/2 * * * *'
    }
    stages {
        stage('Collect Data') {
            steps {
                echo 'clean before any checkout'
                cleanWs()
                echo 'update workspace with latest git repository in default branch master'
                git 'https://github.com/alexkaos87/BankOCR.git'
            }
        }
        stage('Execute Static Analysis') {
            parallel {
                stage('Execute Defects Analysis') {
                    steps {
                        echo 'run cppcheck on source files'
                        sh 'cppcheck BankOCR/ --enable=warning,style,performance --xml --xml-version=2 2> cppcheck-result.xml'
                        echo 'collect cppcheck results'
                        zip archive: true, defaultExcludes: false, dir: '', exclude: '', glob: 'cppcheck-result.xml', zipFile: 'cppcheck-results.zip'
                    }
                }
                stage('Execute Green Analysis') {
                    steps {
                        echo 'run Capgemini GreenSW on source files'
                        sh 'GSWTool BankOCR/OCR.cpp > greensw-results.txt' 
                        zip archive: true, defaultExcludes: false, dir: '', exclude: '', glob: 'greensw-results.txt', zipFile: 'greensw-results.zip'
                    }
                }
            }
        }
    }
    post {
        always {
            publishCppcheck pattern:'cppcheck-result.xml'
            emailext body: '''$PROJECT_NAME - Build # $BUILD_NUMBER - $BUILD_STATUS:

Check console output at $BUILD_URL to view the results.''', subject: '$PROJECT_NAME - Build # $BUILD_NUMBER - $BUILD_STATUS!', to: 'alessio.coppola@capgemini.com'
        }
    }
}
