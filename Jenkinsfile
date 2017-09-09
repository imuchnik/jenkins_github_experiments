pipeline {
  agent any
  stages {
    stage('hello') {
      steps {
        parallel(
          "hello": {
            echo 'Hello World'
            
          },
          "Git commit": {
            script {
              gitCommit = sh(returnStdout: true, script: 'git rev-parse HEAD').trim()
              // short SHA, possibly better for chat notifications, etc.
              shortCommit = gitCommit.take(6)
              println gitCommit
              println shortCommit
            }
            
            
          }
        )
      }
    }
    stage('Package') {
      steps {
        parallel(
          "Package": {
            sleep 40
            sh '''echo $(date) > gigantic_binary.txt
echo "Packaging finished"'''
            
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
    stage('Push to S3') {
      steps {
        sh 'echo "Pushing ${gitCommit} to S3" '
      }
    }
  }
}