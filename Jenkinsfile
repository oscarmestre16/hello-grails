pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                configFileProvider(
                    [configFile(fileId: 'hello-grails-gradle.properties', variable: 'gradle_properties')]) {
                    sh 'mvn -s $gradle_properties clean package'
                }
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
                    
                }
            }

        }
    }
} 

