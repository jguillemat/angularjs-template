@Library('github.com/victornc83/jenkins-library@master') _

nodejsTemplate('sis-devel'){
  def sonarUrl = env.SONAR_URL
  def version = env.CHANGE_ID
  def repourl = ""
  def appName = 'angular'
  def namespace = 'sis-devel'

  stage('Git Checkout'){
    echo "Checking out git repository"
    checkout scm
    repourl = sh(script: "git config --get remote.origin.url", returnStdout: true).trim()
  }

  stage('Build'){
    echo "Building project"
    sh '''
    npm install grunt
    npm install grunt-cli
    export PATH=$PATH:node_modules/grunt-cli/bin/
    grunt
    '''
  }

  stage('Unit Tests') {
    echo "Running Unit Tests"
  }

  stage('Analysis'){
  }

  stage('Deploy in Dev'){
  }

  stage('Integration Tests'){
    echo "Running integration tests"
  }

  stage('Exposing service in Dev'){
    echo "Creating route in Dev"
  }
}
