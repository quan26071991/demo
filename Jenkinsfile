pipeline {
    agent any
    tools {
        maven 'M3'
    }
    stages {
        stage ('Clean and Checkout source') {
            steps {
                dir('/home/quan/.jenkins/workspace/demo'){
                    sh 'git clean -fdx'
                    sh "git pull origin master"
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
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
        stage('Send mail') {
            steps {
                echo 'Sending email....'
            }
        }
    }
}