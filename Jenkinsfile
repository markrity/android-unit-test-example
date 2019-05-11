pipeline {
    agent { docker { 
        image 'anthonymonori/android-ci-image'
        args '-u root:sudo'
        }
    }
    stages {
    stage('Git') {
      // Get some code from a GitHub repository
      steps{
          git 'https://github.com/markrity/android-unit-test-example.git'
      }
   }

    stage('Run Tests'){
          steps{
               sh """
               yes | sdkmanager --licenses
                ./gradlew test
                """
          }
    }
    
    stage('Publish Test Results'){
        steps{
            publishHTML([allowMissing: false, alwaysLinkToLastBuild: true, keepAll: true, reportDir: 'app/build/reports/tests/testReleaseUnitTest', reportFiles: 'index.html', reportName: 'HTML Report', reportTitles: ''])
        }
    }
    
}
}
