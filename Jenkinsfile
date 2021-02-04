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
                    publishHTML(
                        target: [
                            allowMissing            : firefoxHeadless,
                            alwaysLinkToLastBuild   : false,
                            keepAll                 : true,
                            reportDir               : 'build/test-results/test/TEST-*.xml',
                            reportFiler             : '*.html',
                            reportName              : 'Codenarc Report'
                        ]
                    )
                }
            }

        }
    }
} 

