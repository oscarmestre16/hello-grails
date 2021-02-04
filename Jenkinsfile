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
            port{
                always{
                    junit 'build/test-results/test/TEST-*.xml'
                }
            }

        }
    }
} 

