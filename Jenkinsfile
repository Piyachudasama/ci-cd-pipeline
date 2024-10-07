post {
    always {
        mail to: 'piyachudasama222@gmail.com',
             subject: "Pipeline Status: ${currentBuild.currentResult}",
             body: "The pipeline has completed with status: ${currentBuild.currentResult}. Build details: ${env.BUILD_URL}"
    }
}
