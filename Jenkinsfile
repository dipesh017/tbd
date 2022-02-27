pipeline{
    agent { label 'worker' } 
    options {
        buildDiscarder(logRotator(daysToKeepStr: '15'))
        timeout(time: 1, unit: 'MINUTES')
        retry(3)
        disableConcurrentBuilds()
    } 
    parameters{
        string(name: 'BRANCH', defaultValue: 'master', description: "Enter the branch here")
        choice(name: 'OPERATION', choices: ['A','S','M','D'])
    }
    stages{
        stage('Git Pull'){
            steps{
                checkout scm
            }
        }
        stage('Unit Testing'){
            steps{
                sh "echo doing unit testing"
                sh "sleep 2"
            }
        }
        stage('Docker Build'){
            steps{
                sh "echo docker build"
            }
        }
    }
    post{
        always{
        echo "Cleaning up ${WORKSPACE}"
        // clean up our workspace 
        deleteDir()           
        }
    }
}
