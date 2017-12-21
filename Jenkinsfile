pipeline {
  agent any
  stages {
    stage('hello') {
      steps {
        echo 'Hello World'
        script {
            gitCommit = "foo"
            env.GIT_COMMIT = gitCommit
            println gitCommit
         }
        echo sh(returnStdout: true, script: 'export GIT_COMMIT="foo1"')
        sh 'printenv'
        withEnv(['GIT_COMMIT="foo"']){
            echo sh(returnStdout: true, script: 'env')
        }
      }
    }
    stage('million'){
        steps{
            echo sh(returnStdout: true, script: "echo ${env.GIT_COMMIT}")
        }
     }
  }
}