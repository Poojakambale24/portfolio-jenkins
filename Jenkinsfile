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
            }
        }

        stage('Deploy') {
            steps {
                powershell '''
                    Write-Host "Deploying to C:\\deploy\\portfolio"

                    if (Test-Path "C:\\deploy\\portfolio") {
                        Remove-Item -Recurse -Force "C:\\deploy\\portfolio"
                    }

                    New-Item -ItemType Directory -Force -Path "C:\\deploy\\portfolio"

                    Copy-Item -Path "$env:WORKSPACE\\*.html" -Destination "C:\\deploy\\portfolio" -Force
                    Copy-Item -Path "$env:WORKSPACE\\*.css" -Destination "C:\\deploy\\portfolio" -Force
                '''
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
