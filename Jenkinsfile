pipeline {
  agent any
  options {
    disableConcurrentBuilds()
    timestamps()
  }
  environment {
    // Adjust this path for your deployment target (Linux example)
    DEPLOY_PATH = '/var/www/html/portfolio'
  }
  triggers {
    // Requires GitHub plugin. Webhook will call /github-webhook/
    githubPush()
    // Optional: pollSCM('@daily')
  }
  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }
    stage('Validate') {
      steps {
        echo 'Validation placeholder: add HTML/CSS/link checks here.'
        script {
          if (isUnix()) {
            sh 'echo "Running on Unix node"'
          } else {
            bat 'echo Running on Windows node'
          }
        }
      }
    }
    stage('Deploy') {
      steps {
        script {
          if (isUnix()) {
            sh '''
              echo "Deploying to $DEPLOY_PATH"
              mkdir -p "$DEPLOY_PATH"
              cp -v index.html about.html style.css "$DEPLOY_PATH"/
            '''
          } else {
            bat '''
              echo Deploying to %DEPLOY_PATH%
              if not exist %DEPLOY_PATH% mkdir %DEPLOY_PATH%
              copy /Y index.html %DEPLOY_PATH%\
              copy /Y about.html %DEPLOY_PATH%\
              copy /Y style.css %DEPLOY_PATH%\
            '''
          }
        }
      }
    }
    stage('Archive') {
      steps {
        archiveArtifacts artifacts: 'index.html,about.html,style.css', fingerprint: true
      }
    }
  }
  post {
    success {
      echo 'Build succeeded.'
    }
    failure {
      echo 'Build failed.'
    }
  }
}
