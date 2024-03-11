pipeline {
    agent any

    triggers {
        cron('H/10 * * * 1')
    }

    tools {
        maven 'maven'
    }

    stages {
        stage('Build') {
            steps {
                tool 'Maven'
                bat 'mvn clean package'
            }
        }

        stage('Test with JaCoCo') {
            steps {
                tool 'Maven'
                bat 'mvn test jacoco:report'
            }

            post {
                always {
                    jacoco execPattern: '**/target/jacoco.exec', classPattern: '**/classes', sourcePattern: '**/src/main/java'
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