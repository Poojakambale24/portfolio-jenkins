pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Validate') {
            steps {
                echo "Validation placeholder: add HTML/CSS checks here"
                bat 'echo Running on Windows node'
            }
        }

        stage('Deploy') {
            steps {
                script {
                    bat '''
                    echo Deploying to C:\\deploy\\portfolio

                    if exist C:\\deploy\\portfolio rmdir /S /Q C:\\deploy\\portfolio
                    mkdir C:\\deploy\\portfolio

                    xcopy /E /Y "%WORKSPACE%\\*.html" "C:\\deploy\\portfolio\\"
                    xcopy /E /Y "%WORKSPACE%\\*.css" "C:\\deploy\\portfolio\\"
                    '''
                }
            }
        }

        stage('Archive') {
            steps {
                archiveArtifacts artifacts: '**/*.html, **/*.css', fingerprint: true
            }
        }
    }

    post {
        success {
            echo 'Deployment completed successfully.'
        }
        failure {
            echo 'Build failed.'
        }
    }
}
