pipeline {
    agent any
    triggers {
        upstream 'Weekly Overall Check, '
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
        stage('Compile') {
            steps {
                echo 'compile source code and tests executable'
                sh 'rm -rf build'
                sh 'mkdir build'
                cmakeBuild buildDir: 'build', cleanBuild: true, installation: 'InSearchPath', steps: [[args: 'all']]
                echo 'collect build data as zip and save as artifact'
                zip archive: true, defaultExcludes: false, dir: 'build', exclude: '', glob: '', zipFile: 'build.zip'
            }
        }
        stage('Run Unit Tests') {
            steps {
                echo 'run gtest from command line'
                sh './build/BankOCRTests'
                zip archive: true, defaultExcludes: false, dir: '', exclude: '', glob: 'tests-result.xml', zipFile: 'tests-result.zip'
            }
        }
    }
    post {
        always {
            junit allowEmptyResults: true, skipOldReports: true, testResults: 'tests-result.xml'
            emailext body: '''$PROJECT_NAME - Build # $BUILD_NUMBER - $BUILD_STATUS:

Check console output at $BUILD_URL to view the results.''', subject: '$PROJECT_NAME - Build # $BUILD_NUMBER - $BUILD_STATUS!', to: 'alessio.coppola@capgemini.com'
        }
    }
}
