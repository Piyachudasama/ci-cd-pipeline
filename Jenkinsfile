pipeline {
    agent any

    environment {
        RECIPIENT_EMAIL = 'piyachudasama92@gmail.com'
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building the application using Maven...'
                // sh 'mvn clean package'
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit and integration tests with JUnit...'
                // sh 'mvn test'
            }
            post {
                always {
                    emailext(
                        subject: "Test Stage: ${currentBuild.currentResult}",
                        body: "The test stage has completed with status: ${currentBuild.currentResult}.",
                        to: "${RECIPIENT_EMAIL}",
                        mimeType: 'text/plain',
                        attachLog: true
                    )
                }
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Performing code analysis using SonarQube...'
                // sh 'sonar-scanner'
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Running security scan using OWASP Dependency-Check...'
                // sh 'dependency-check --scan .'
            }
            post {
                always {
                    emailext(
                        subject: "Security Scan Stage: ${currentBuild.currentResult}",
                        body: "The security scan stage has completed with status: ${currentBuild.currentResult}.",
                        to: "${RECIPIENT_EMAIL}",
                        mimeType: 'text/plain',
                        attachLog: true
                    )
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Deploying application to the staging environment on AWS...'
                // sh 'aws deploy my-app-staging'
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on the staging environment...'
                // sh './run-staging-tests.sh'
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Deploying application to the production environment on AWS...'
                // sh 'aws deploy my-app-production'
            }
        }
    }

    post {
        always {
            echo "Pipeline execution completed."
        }
    }
}
