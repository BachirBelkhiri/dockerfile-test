pipeline {
    agent any


    stages {
        
        stage('SCM Poll') {
            //agent { dockerfile true }
            steps {
                //git 'https://github.com/BachirBelkhiri/dockerfile-test.git'
                sh 'ls -ali'
            }
            
            post {
                success {
                    slackSend teamDomain: 'letshavesomefundudes', channel: '#devops', color: '#008000', tokenCredentialId: 'slack-token',  failOnError: true, message: "Git Cloned ${env.JOB_NAME} ${env.BUILD_NUMBER} (<${env.BUILD_URL}|Open>)"
                }
            }

        }

        stage('Build') {
            agent { 
                dockerfile { 
                    filename 'Dockerfile'
                    //dir 'build'
                }
            }
            
            steps {
                sh 'node --version'
                sh 'git --version'
                sh 'curl --version'
            }
            
            post {
                always {
                    // I will always be executed
                    //echo "Hello world"
                }
                        
                success {
                    // I will be executed if i success
                    slackSend teamDomain: 'letshavesomefundudes', channel: '#devops', color: 'good', tokenCredentialId: 'slack-token',  failOnError: true, message: "Build Success ${env.JOB_NAME} ${env.BUILD_NUMBER} (<${env.BUILD_URL}|Open>)"
                }
                
                failure {
                    // I will be executed if i fail
                    slackSend teamDomain: 'letshavesomefundudes', channel: '#devops', color: 'danger', tokenCredentialId: 'slack-token',  failOnError: true, message: "Build Fail ${env.JOB_NAME} ${env.BUILD_NUMBER} (<${env.BUILD_URL}|Open>)"
                }
                
                //changed {
                    // I will be executed if something chnage from the previous build
                //}
                
                //fixed {
                    // I will be executed if i am fixed from the previous build
                //}
                
                //aborted {
                    // I will be executed if i am aborted
                //}
                
                
            }
            
        }
    }
}
