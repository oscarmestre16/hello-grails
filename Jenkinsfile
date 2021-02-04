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
                    configFileProvider(
                        [configFile(fileId: 'hello-grails-gradle.properties', targetLocation: 'gradle.properties')])         {
                            sh './gradlew integrationTest'
                        }
                }
            }
            post{
                always{
                    junit 'build/test-results/test/TEST-*.xml'

                    publishHTML (
                        target : [
                        
                        alwaysLinkToLastBuild: true,
                        keepAll: true,
                        reportDir: 'build/reports/',
                        reportFiles: 'myreports.html',
                        reportName: 'My Reports',
                        reportTitles: 'Codenarc Report'
                    ])
                    
                }
            }

        }
    }
} 

