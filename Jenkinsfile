#!groovy

pipeline {
  agent { 
    dockerfile {
      args "-v /etc/group:/etc/group:ro -v /etc/passwd:/etc/passwd:ro -v /etc/shadow:/etc/shadow:ro"
    }
  }

  options {
    quietPeriod(120)
    disableConcurrentBuilds()
  }

  stages {
    stage('Deploy to Github Pages') {
      when { branch 'master' }
      options {
        skipDefaultCheckout true
      }
      steps {
        sh "git config remote.origin.url git@github.com:zooniverse/help.git"
        sshagent(credentials: ["cd5582ce-30e3-49bb-8b04-a1a5d1ff7b56"]) {
          sh "mkdocs gh-deploy"
        }
      }
    }
  }
}
