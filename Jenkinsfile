pipeline {
    agent any
    triggers {
      cron('*/15 * * * *') // at the 23:59 of every day H 23 * * *
    }
    environment {
        changedFilesToAnalize = ''
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
        stage('Retrieve Changed Files') {
            steps {
                script {
                    // Retrieve the list of changed files during the day using git diff command
                    def changedFiles = sh(returnStdout: true, script: "git diff --name-only --since='start of day'").trim()
                    changedFilesToAnalize = ''

                    // Split the changed files into a list
                    def changedFilesList = changedFiles.split('\n')

                    // Print the list of changed files
                    for (file in changedFilesList) {
                        echo file
                        
                        if (file.endsWith(".cpp") || file.endsWith(".cxx") || file.endsWith(".cc") || file.endsWith(".c") || file.endsWith(".h") || file.endsWith(".hpp")) {
                            changedFilesToAnalize = changedFilesToAnalize + file + " "
                        }                        
                    }
                }
            }
        }
        stage('Execute Static Analysis') {
			parallel {
				stage('Execute Defects Analysis') {
					steps {
                        script {
                            echo 'run cppcheck on source files'
                            if (env.changedFilesToAnalize == null || env.changedFilesToAnalize.isEmpty()) {
                                echo 'no changed files available'
                            }
                            else {
                                sh "cppcheck ${env.changedFilesToAnalize} --enable=warning,style,performance --xml --xml-version=2 2> cppcheck-result.xml"
                                echo 'collect cppcheck results'
                                zip archive: true, defaultExcludes: false, dir: '', exclude: '', glob: 'cppcheck-result.xml', zipFile: 'cppcheck-results.zip'
                            }
                        }
					}
		//			post {
		//				always {
		//					publishCppcheck pattern:'cppcheck-result.xml'
		//				}
		//			}
				}
				stage('Execute Green Analysis') {
    				steps {
                        script {
                            echo 'run Capgemini GreenSW on source files'
                            if (env.changedFilesToAnalize == null || env.changedFilesToAnalize.isEmpty()) {
                                echo 'no changed files available'
                            }
                            else {
                                sh 'GSWTool BankOCR/OCR.cpp > greensw-results.txt' 
                                zip archive: true, defaultExcludes: false, dir: '', exclude: '', glob: 'greensw-results.txt', zipFile: 'greensw-results.zip'
                            }
                        }
    				}
				}
            }
        }
    }
    //post {
    //    always {
     //       emailext body: '''$PROJECT_NAME - Build # $BUILD_NUMBER - $BUILD_STATUS:
//
//Check console output at $BUILD_URL to view the results.''', subject: '$PROJECT_NAME - Build # $BUILD_NUMBER - $BUILD_STATUS!', to: 'alessio.coppola@capgemini.com'
//        }
//    }
}
