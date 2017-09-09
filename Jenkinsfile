pipeline {
  agent any
  stages {
    stage('hello') {
      steps {
        echo 'Hello World'
      }
    }
    stage('Package') {
      steps {
        parallel(
          "Package": {
            sleep 40
            sh 'echo "Packaging finished"'
            sh 'echo "Pushing to S3"'
            
          },
          "Security Tests": {
            sleep 30
            sh 'echo "Security Tests Finished"'
            
          },
          "Unit Tests": {
            sleep 10
            sh 'echo "Unit Tests Finished"'
            
          },
          "Goodbye": {
            sleep 41
            sh 'echo "Goodbye"'
            
          }
        )
      }
    }
  }
}