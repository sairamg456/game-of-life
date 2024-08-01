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
    parameters {
        choice(name: 'GOAL', choices: ['package', 'clean package', 'install', 'clean install'], description: 'this mvn package')
    }
    tools {
        jdk 'JDK_8'
    }
    stages {
        stage ('vcs'){
            steps {
                git url: 'https://github.com/sairamg456/game-of-life.git',
                    branch: 'master'
            }
        }
        stage ('build and package'){
            steps {
                sh script: "mvn ${params.GOAL}"
            }
        }
        stage ('test results'){
            steps {
                junit testResults: '**/surefire-reports/TEST-*.xml'
                archiveArtifacts artifacts: '**/target/gameoflife*.war'
            }
        }
    }
    post {
        success {
            mail subject: "${JOB_NAME} is effective",
                 body: "Project build url is ${BUILD_URL}",
                 to: 'all@jenkins.com'
        }
        failure {
            mail subject: "${JOB_NAME} is deffective",
                 body: "Project build url is ${BUILD_URL}",
                 to: 'all@jenkins.com'
        }
    }
}