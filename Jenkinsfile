pipeline {
    agent any

    environment {
        RECIPIENT_EMAIL = 'piyachudasama92@gmail.com'
    }

    stages {
        stage('Build Application') {
            steps {
                echo 'Building the application...'
                // Replace this with actual build commands
                // Example: sh 'mvn clean install'
            }
        }

        stage('Run Unit and Integration Tests') {
            steps {
                echo 'Running unit and integration tests...'
                // Replace this with actual test commands
                // Example: sh 'mvn test'
            }
            post {
                always {
                    echo "Sending test result email to: ${RECIPIENT_EMAIL}"
                    emailext(
                        subject: "Test Result: ${currentBuild.currentResult} for ${env.JOB_NAME} - Build #${env.BUILD_NUMBER}",
                        body: """
                            <p>Test result: <b>${currentBuild.currentResult}</b></p>
                            <p>Build URL: <a href="${env.BUILD_URL}">${env.BUILD_URL}</a></p>
                            """,
                        to: "${RECIPIENT_EMAIL}",
                        mimeType: 'text/html',
                        attachLog: true
                    )
                    echo "Test result email sent to: ${RECIPIENT_EMAIL}"
                }
            }
        }

        stage('Deploy Application') {
            steps {
                echo 'Deploying the application...'
                // Replace this with actual deployment commands
            }
        }
    }

    post {
        always {
            echo "Sending final pipeline status email to: ${RECIPIENT_EMAIL}"
            emailext(
                subject: "Pipeline Completed: ${env.JOB_NAME} - Build #${env.BUILD_NUMBER}",
                body: """
                    <p>Pipeline status: <b>${currentBuild.currentResult}</b></p>
                    <p>Build URL: <a href="${env.BUILD_URL}">${env.BUILD_URL}</a></p>
                    """,
                to: "${RECIPIENT_EMAIL}",
                mimeType: 'text/html',
                attachLog: true
            )
            echo "Final pipeline status email sent to: ${RECIPIENT_EMAIL}"
        }

        success {
            echo "Sending success email to: ${RECIPIENT_EMAIL}"
            emailext(
                subject: "SUCCESS: ${env.JOB_NAME} - Build #${env.BUILD_NUMBER}",
                body: """
                    <p>The build was successful for ${env.JOB_NAME} - Build #${env.BUILD_NUMBER}</p>
                    <p>Build URL: <a href="${env.BUILD_URL}">${env.BUILD_URL}</a></p>
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
                    <p>The build failed for ${env.JOB_NAME} - Build #${env.BUILD_NUMBER}</p>
                    <p>Build URL: <a href="${env.BUILD_URL}">${env.BUILD_URL}</a></p>
                    """,
                to: "${RECIPIENT_EMAIL}",
                mimeType: 'text/html',
                attachLog: true
            )
            echo "Failure email sent to: ${RECIPIENT_EMAIL}"
        }
    }
}
