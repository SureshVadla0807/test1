
pipeline {
    agent any

    triggers {
        pollSCM('H/2 * * * *')
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'Source code checked out'
            }
        }

        stage('Build') {
            steps {
                bat 'echo Building HTML application'
                bat 'dir'
            }
        }

        stage('Test') {
            steps {
                bat 'if not exist index.html exit /b 1'
                echo 'HTML file verified!'
            }
        }

        stage('Deploy') {
            steps {
                bat '''
                if not exist deployment mkdir deployment
                copy /Y index.html deployment\\
                '''
                archiveArtifacts artifacts: 'deployment/**'
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
