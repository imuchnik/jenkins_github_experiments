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
              gitCommit = "foo"
              env.GIT_COMMIT = gitCommit
              println gitCommit
            }
          },
          sh 'printenv',
          withEnv(['GIT_COMMIT="foo:']),
          echo sh(returnStdout: true, script: 'env')
        )
      }
    }
    stage('Test and Package') {
      steps {
        parallel(
          "Package": {
            sleep 3
            sh '''
echo $(date) > gigantic_binary.txt
echo "Packaging finished"'''
            archiveArtifacts(artifacts: 'gigantic*.*', fingerprint: true, onlyIfSuccessful: true)
            
          },
          "Security Tests": {
            sleep 2
            sh 'echo "Security Tests Finished"'
            
          },
          "Unit Tests": {
            sleep 1
            sh 'echo "Unit Tests Finished"'
            
          }
        )
      }
    }
    stage('Push to S3') {
      steps {
        parallel(
          "Push to S3": {
            sh 'echo "Pushing git commit to S3" '
            
          },
          "Push to S3 Groovy": {
            script {
              println "Pushing ${env.gitCommit} to S3"
              println "Pushing ${gitCommit} to S3"
            }
          }
        )
      }
    }
  }
}