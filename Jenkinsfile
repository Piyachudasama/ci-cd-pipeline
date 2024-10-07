pipeline {
    agent any

    environment {
        RECIPIENT_EMAIL = 'piyachudasama222@gmail.com'
    }

    stages {
        stage('Build Application') {
            steps {
                echo 'Starting the build process with Maven...'
                // sh 'mvn clean install'
            }
        }
        stage('Run Unit and Integration Tests') {
            steps {
                echo 'Running unit and integration tests using JUnit and Selenium...'
                // sh 'mvn test'
            }
            post {
                success {
                    emailext(
                        subject: "SUCCESS: Unit & Integration Tests for ${env.JOB_NAME} - Build #${env.BUILD_NUMBER}",
                        body: """<p>All unit and integration tests have passed for the project <b>${env.JOB_NAME}</b>.</p>
                                 <p>Logs are attached for further review.</p>""",
                        to: "${RECIPIENT_EMAIL}",
                        mimeType: 'text/html',
                        attachLog: true
                    )
                }
                failure {
                    emailext(
                        subject: "FAILURE: Unit & Integration Tests for ${env.JOB_NAME} - Build #${env.BUILD_NUMBER}",
                        body: """<p>There was a failure in the unit and integration tests for the project <b>${env.JOB_NAME}</b>.</p>
                                 <p>Please check the attached logs for detailed information.</p>""",
                        to: "${RECIPIENT_EMAIL}",
                        mimeType: 'text/html',
                        attachLog: true
                    )
                }
            }
        }
        stage('Perform Static Code Analysis') {
            steps {
                echo 'Running static code analysis using SonarQube...'
                // sh 'sonar-scanner'
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Running security scan with OWASP Dependency-Check...'
                // sh 'dependency-check --scan .'
            }
            post {
                success {
                    emailext(
                        subject: "SUCCESS: Security Scan for ${env.JOB_NAME} - Build #${env.BUILD_NUMBER}",
                        body: """<p>The security scan for <b>${env.JOB_NAME}</b> was completed successfully.</p>
                                 <p>Please review the attached logs for more details.</p>""",
                        to: "${RECIPIENT_EMAIL}",
                        mimeType: 'text/html',
                        attachLog: true
                    )
                }
                failure {
                    emailext(
                        subject: "FAILURE: Security Scan for ${env.JOB_NAME} - Build #${env.BUILD_NUMBER}",
                        body: """<p>The security scan for <b>${env.JOB_NAME}</b> encountered issues and failed.</p>
                                 <p>Logs have been attached for your review.</p>""",
                        to: "${RECIPIENT_EMAIL}",
                        mimeType: 'text/html',
                        attachLog: true
                    )
                }
            }
        }
        stage('Deploy to Staging Environment') {
            steps {
                echo 'Deploying the application to the staging environment...'
                // sh 'aws deploy staging-app'
            }
        }
        stage('Run Staging Tests') {
            steps {
                echo 'Running integration tests on the staging environment...'
                // sh './run-staging-tests.sh'
            }
        }
        stage('Deploy to Production Environment') {
            steps {
                echo 'Deploying the application to the production environment...'
                // sh 'aws deploy production-app'
            }
        }
    }

    post {
        success {
            emailext(
                subject: "SUCCESS: Pipeline Execution for ${env.JOB_NAME} - Build #${env.BUILD_NUMBER}",
                body: """<p>The Jenkins pipeline for <b>${env.JOB_NAME}</b> was successfully completed.</p>
                         <p>Logs are attached for review.</p>""",
                to: "${RECIPIENT_EMAIL}",
                mimeType: 'text/html',
                attachLog: true
            )
        }
        failure {
            emailext(
                subject: "FAILURE: Pipeline Execution for ${env.JOB_NAME} - Build #${env.BUILD_NUMBER}",
                body: """<p>The Jenkins pipeline for <b>${env.JOB_NAME}</b> failed.</p>
                         <p>Please check the attached logs for more information.</p>""",
                to: "${RECIPIENT_EMAIL}",
                mimeType: 'text/html',
                attachLog: true
            )
        }
        always {
            echo 'Pipeline execution completed.'
        }
    }
}
