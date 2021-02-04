pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                withGradle{
                    sh './gradlew assemble'
                }
            }
        }
        stage('Test') {
            steps {
                withGradle{
                    sh './gradlew clean test'
                    sh './gradlew -Dgeb.env=firefoxHeadless iT'
                    sh './gradlew codenarcTest'
                }
            }
            post{
                always{
                    junit 'build/test-results/test/TEST-*.xml'
                    echo 'Publish Codenarc report'
                    publishHTML (
                        target : [
                        allowMissing: firefoxHeadless,
                        alwaysLinkToLastBuild: true,
                        keepAll: true,
                        reportDir: 'build/test-results/test/TEST-*.xml',
                        reportFiles: '*.html',
                        reportName: 'My Reports',
                        reportTitles: 'Codenarc Report'])
                }
            }

        }
    }
} 

