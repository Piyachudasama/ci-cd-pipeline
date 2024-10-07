pipeline {
    agent any

    environment {
        RECIPIENT_EMAIL = 'piyachudasama92@gmail.com'
    }

    stages {
        stage('Build Application') {
            steps {
                echo 'Building the application...'
                // Add your build commands here, for example: sh 'mvn clean install'
            }
        }

        stage('Run Unit and Integration Tests') {
            steps {
                echo 'Running unit and integration tests...'
                // Add your test commands here, for example: sh 'mvn test'
            }
        }

        stage('Deploy Application') {
            steps {
                echo 'Deploying the application...'
                // Add your deployment commands here
            }
        }
    }

    post {
        always {
            echo "Attempting to send email notification to: ${RECIPIENT_EMAIL}"
            emailext(
                subject: "Pipeline Status: ${currentBuild.currentResult} - ${env.JOB_NAME} Build #${env.BUILD_NUMBER}",
                body: """
                    Build Status: <strong>${currentBuild.currentResult}</strong><br>
                    Project: ${env.JOB_NAME} <br>
                    Build Number: ${env.BUILD_NUMBER} <br>
                    Build URL: <a href="${env.BUILD_URL}">${env.BUILD_URL}</a><br>
                    Check the attached build log for details.
                """,
                to: "${RECIPIENT_EMAIL}",
                mimeType: 'text/html',
                attachLog: true
            )
            echo "Email notification attempt completed for: ${RECIPIENT_EMAIL}"
        }

        success {
            echo "Sending success email to: ${RECIPIENT_EMAIL}"
            emailext(
                subject: "SUCCESS: ${env.JOB_NAME} Build #${env.BUILD_NUMBER}",
                body: """
                    The build was successful for ${env.JOB_NAME} - Build #${env.BUILD_NUMBER}.<br>
                    Build URL: <a href="${env.BUILD_URL}">${env.BUILD_URL}</a>
                """,
                to: "${RECIPIENT_EMAIL}",
                mimeType: 'text/html',
                attachLog: true
            )
            echo "Success email sent to: ${RECIPIENT_EMAIL}"
        }

        failure {
            echo "Sending failure email to: ${RECIPIENT_EMAIL}"
            emailext(
                subject: "FAILURE: ${env.JOB_NAME} Build #${env.BUILD_NUMBER}",
                body: """
                    The build failed for ${env.JOB_NAME} - Build #${env.BUILD_NUMBER}.<br>
                    Build URL: <a href="${env.BUILD_URL}">${env.BUILD_URL}</a>
                """,
                to: "${RECIPIENT_EMAIL}",
                mimeType: 'text/html',
                attachLog: true
            )
            echo "Failure email sent to: ${RECIPIENT_EMAIL}"
        }
    }
}
