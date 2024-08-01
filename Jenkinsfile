pipeline {
    agent 
    { 
     label 'JDK'}
    options {
        timeout(time: 30, unit: 'MINUTES')
    }
    triggers {
        pollSCM('* * * * *')
    }
    tools {
        jdk 'JDK_8'
    }
    stages {
        stage ('vcs'){
            steps {
                git url: 'https://github.com/sairamg456/game-of-life.git'
                    branch: 'master'
            }
        }
        stage ('build and package'){
            steps {
                sh script: 'mvn package'
            }
        }
        stage ('test results'){
            steps {
                junit testResults: '**/surefire-reports/TEST-*.xml'
                archiveArtifacts artifacts: '**/target/gameoflife*.war'
            }
        }
    }
}