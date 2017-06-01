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
    npm install phantomjs-prebuilt
    npm install
    npm install grunt
    npm install grunt-cli
    export PATH=$PATH:node_modules/grunt-cli/bin/
    grunt
    '''
  }

  stage('Tests'){
    echo "Running tests"
  }

  stage('Image creation') {
    echo "Creating new image"
    sh "mkdir oc-build ; cp -R build/* oc-build/"
    startBuild(namespace,appName)
    echo "This is the build number: ${env.BUILD_NUMBER}"
  }

  stage('Deploy in Dev'){
    echo "Deploy application"
    waitDeployIsComplete(namespace,appName)
  }

  stage('Integration Tests'){
    echo "Running integration tests"
  }

  stage('Exposing service in Dev'){
    echo "Creating route in Dev"
    exposeSvc{
      name=appName
      project=namespace
    }
  }
}
