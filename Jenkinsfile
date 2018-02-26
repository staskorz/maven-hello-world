pipeline {
    agent any

    stages {
        stage('Clean') {
            steps {
                dir('my-app') {
                    mvn clean
                }
            }
        }
    }

    post {
        always {
            mail(
                to: "${env.NOTIFY_EMAIL}",
                subject: "Job '${env.JOB_NAME}' status '${currentBuild.currentResult}'",
                body: "Job '${env.JOB_NAME}' complete with status '${currentBuild.currentResult}'"
            )
        }
    }
}
