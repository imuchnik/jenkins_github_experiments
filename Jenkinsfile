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
          "Test and Package": {
            sleep 3
            sh '''echo $(date) > gigantic_binary.txt
echo "Packaging finished"'''
            
          },
          "Security Tests": {
            sleep 2
            sh 'echo "Security Tests Finished"'
            
          },
          "Unit Tests": {
            sleep 1
            sh 'echo "Unit Tests Finished"'
            
          },
          "Goodbye": {
            sleep 4
            sh 'echo "Goodbye"'
            
          }
        )
      }
    }
    stage('Push to S3') {
      steps {
        parallel(
          "Push to S3": {
            sh 'echo "Pushing ${gitCommit} to S3" '
            
          },
          "Push to S3 Groovy": {
            script {
              println "Pushing ${gitCommit} to S3"
            }
            
            
          }
        )
      }
    }
  }
}