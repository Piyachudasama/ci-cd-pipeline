pipeline {
    agent any

    environment {
        RECIPIENT_EMAIL = 'piyachudasama92@gmail.com'
    }

    stages {
        stage('Build Application') {
            steps {
                echo 'Building the application...'
                // Uncomment the following line to add actual build command
                // sh 'mvn clean install'
            }
        }

        stage('Run Unit and Integration Tests') {
            steps {
                echo 'Running unit and integration tests...'
                // Uncomment the following line to add actual test command
                // sh 'mvn test'
            }
        }

        stage('Deploy Application') {
            steps {
                echo 'Deploying the application...'
                // Uncomment the following line to add actual deployment command
            }
        }
    }

    post {
        always {
            echo "Sending final pipeline status email to: ${RECIPIENT_EMAIL}"
            emailext(
                subject: "Pipeline Completed: ${env.JOB_NAME} - Build #${env.BUILD_NUMBER}",
                body: "Pipeline ${env.JOB_NAME} - Build #${env.BUILD_NUMBER} completed with result: ${currentBuild.currentResult}. \nCheck logs: ${env.BUILD_URL}",
                to: "${RECIPIENT_EMAIL}",
                mimeType: 'text/plain',
                attachLog: true
            )
            echo "Email sent to: ${RECIPIENT_EMAIL}"
        }

        success {
            echo "Sending success email to: ${RECIPIENT_EMAIL}"
            emailext(
                subject: "SUCCESS: ${env.JOB_NAME} - Build #${env.BUILD_NUMBER}",
                body: "The build was successful for ${env.JOB_NAME} - Build #${env.BUILD_NUMBER}. \nCheck logs: ${env.BUILD_URL}",
                to: "${RECIPIENT_EMAIL}",
                mimeType: 'text/plain',
                attachLog: true
            )
            echo "Success email sent to: ${RECIPIENT_EMAIL}"
        }

        failure {
            echo "Sending failure email to: ${RECIPIENT_EMAIL}"
            emailext(
                subject: "FAILURE: ${env.JOB_NAME} - Build #${env.BUILD_NUMBER}",
                body: "The build failed for ${env.JOB_NAME} - Build #${env.BUILD_NUMBER}. \nCheck logs: ${env.BUILD_URL}",
                to: "${RECIPIENT_EMAIL}",
                mimeType: 'text/plain',
                attachLog: true
            )
            echo "Failure email sent to: ${RECIPIENT_EMAIL}"
        }
    }
}
