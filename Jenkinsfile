pipeline {
    agent any
    stages {
        stage('Build') {
            steps {               
                configFileProvider(
                    [configFile(fileId: 'hello-grails-gradle.properties', targetLocation: 'gradle.properties')])         {
                        sh './gradlew iT'
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

