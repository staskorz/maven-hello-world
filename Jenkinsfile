pipeline {
    agent any

    stages {
        stage('Clean') {
            steps {
                dir('my-app') {
                    sh "mvn clean"
                }
            }
        }

        stage('Package') {
            steps {
                dir('my-app') {
                    sh "mvn package"
                }
            }
        }
    }

    post {
        success {
            archiveArtifacts artifacts: 'my-app/target/*.jar', fingerprint: true
        }

        always {
            mail(
                to: "${env.NOTIFY_EMAIL}",
                subject: "Job '${env.JOB_NAME}' status '${currentBuild.currentResult}'",
                body: "Job '${env.JOB_NAME}' complete with status '${currentBuild.currentResult}'"
            )
        }
    }
}
