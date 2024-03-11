pipeline {
    agent any

    triggers {
        cron('H/10 * * * 1')
    }

    tools {
        maven 'Maven'
    }

    stages {
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Test with JaCoCo') {
            steps {
                sh 'mvn test jacoco:report'
            }

            post {
                always {
                    archiveArtifacts artifacts: 'target/site/jacoco/**/*', allowEmptyArchive: true
                    jacoco reportPath: 'target/site/jacoco/'
                }
            }
        }
    }

    post {
        success {
            echo 'Build was successful!'
        }

        failure {
            echo 'Build failed.'
        }
    }
}
