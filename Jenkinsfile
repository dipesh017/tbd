pipeline{
    agent any
    options {
        buildDiscarder(logRotator(daysToKeepStr: '15'))
        timeout(time: 2, unit: 'MINUTES')
        retry(3)
        disableConcurrentBuilds()
    } 
    parameters{
        string(name: 'BRANCH', defaultValue: 'master', description: "Enter the branch here")
        choice(name: 'OPERATION', choices: ['A','S','M','D'])
    }
    stages{
        stage('New Git Pull'){
            when {
            expression {
                return env.BRANCH.startsWith('run');
            }
            }
            input {
                message "Can we proceed?"
                ok "Yes"
            }
            steps{
                echo "git pull"
            }
        }
        stage('Parallel unit testing'){
            parallel{
                stage('Unit Testing  Linux'){
                    steps{
                        sh "echo doing unit testing"
                        sh "sleep 20"
                    }
                }
                stage('Unit Testing  Windows'){
                    steps{
                        sh "echo doing unit testing"
                        sh "sleep 20"
                    }
                }
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
