pipeline {
    agent any
    tools {
        maven 'M3'
    }
	triggers { // trigger job every 5 minutes
        cron('H/5 * * * *')
    }
    stages {
        stage ('Clean and Checkout source before build') {
            steps {
				echo 'Clean and Checkout source before build..'
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
    }
    post {
        always { //alway show result even if build fail or build success
            echo 'BUILD FINISHED'
        }
        success {
            echo 'BUILD SUCCESS'
        }
        failure {
            echo 'BUILD FAILURE'
        }
    }
}