pipeline {
    agent any

    triggers {
        cron('H/10 * * * 1')
    }

    tools {
        maven 'Maven'
    }

    stage('Report') {
            steps {
                script {
                    sh 'mvn clean test jacoco:report'
                }
            }
            post {
                always {
                    jacoco(
                        execPattern: '**/**.exec',
                        classPattern: '**/classes',
                        sourcePattern: '**/src/main/java',
                        check: [
                            buildOverBuild: true,
                            stability: true
                        ]
                    )
                    publishHTML([
                        allowMissing: false,
                        alwaysLinkToLastBuild: false,
                        keepAll: true,
                        reportDir: 'target/site/jacoco/',
                        reportFiles: 'index.html',
                        reportName: 'JaCoCo Coverage Report',
                        reportTitles: ''
                    ])
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
