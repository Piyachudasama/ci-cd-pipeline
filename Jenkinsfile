pipeline {
    agent any

    environment {
        RECIPIENT_EMAIL = 'piyachudasama222@gmail.com'
    }

    stages {
        stage('Build Application') {
            steps {
                echo 'Building the application...'
                // Uncomment and add your build commands if needed
                // sh 'mvn clean install'
            }
        }

        stage('Run Unit and Integration Tests') {
            steps {
                echo 'Running unit and integration tests...'
                // Uncomment and add your test commands if needed
                // sh 'mvn test'
            }
        }

        stage('Deploy Application') {
            steps {
                echo 'Deploying the application...'
                // Uncomment and add your deployment commands if needed
            }
        }
    }

    post {
        always {
            echo "Attempting to send email notification to: ${RECIPIENT_EMAIL}"
            emailext(
                subject: "Pipeline Completed: ${env.JOB_NAME} - Build #${env.BUILD_NUMBER}",
                body: """
                    <p><strong>Pipeline Status:</strong> ${currentBuild.currentResult}</p>
                    <p><strong>Build Details:</strong> <a href="${env.BUILD_URL}">${env.BUILD_URL}</a></p>
                    <p>Please check the logs for more details.</p>
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
                subject: "SUCCESS: ${env.JOB_NAME} - Build #${env.BUILD_NUMBER}",
                body: """
                    <p>The build was successful for ${env.JOB_NAME} - Build #${env.BUILD_NUMBER}.</p>
                    <p><strong>Build URL:</strong> <a href="${env.BUILD_URL}">${env.BUILD_URL}</a></p>
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
                subject: "FAILURE: ${env.JOB_NAME} - Build #${env.BUILD_NUMBER}",
                body: """
                    <p>The build failed for ${env.JOB_NAME} - Build #${env.BUILD_NUMBER}.</p>
                    <p><strong>Build URL:</strong> <a href="${env.BUILD_URL}">${env.BUILD_URL}</a></p>
                """,
                to: "${RECIPIENT_EMAIL}",
                mimeType: 'text/html',
                attachLog: true
            )
            echo "Failure email sent to: ${RECIPIENT_EMAIL}"
        }
    }
}
