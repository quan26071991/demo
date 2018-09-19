pipeline {
    agent any
    tools {
        maven 'M3'
    }
	triggers {
        cron('H/30 * * * *')
    }
    stages {
        stage ('Clean source before build') {
            steps {
                dir('/home/quan/.jenkins/workspace/demo'){
                    sh 'git clean -fdx'
                }
            }
        }
        stage ('Clean Build') {
            steps {
                dir('/home/quan/.jenkins/workspace/demo'){
                    sh "mvn clean"
                }
            }
        }
        stage('Builds') {
            steps {
                echo 'Building..'
                dir('/home/quan/.jenkins/workspace/demo'){
                    sh "mvn install -DskipTests"
                }

            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
                dir('/home/quan/.jenkins/workspace/demo'){
                    sh "mvn surefire:test"
                }
            }
        }
        stage('Send mail') {
            steps {
                echo 'Sending email....'
            }
        }
    }
    post { 
        always { 
            echo 'I have finished!'
        }
        success {
            echo 'I succeeeded'
        }
        failure {
            echo 'I failed'
        }
    }
}