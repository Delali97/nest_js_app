pipeline {

    agent any

    stages {
        stage("environment preparation"){
            steps {
                sh "pwd"
                sh "ls"
                sh "echo ${USER}"
                sh "df -h"
                sh "curl ifconfig.co"
                sh "echo testing"
            }
        }

        stage("connect to deploy server"){

            environment { 
                SSH_CRED = credentials('jenkinstest-pem')
            }

            steps {
                //=============== THIRD APPROACH
                script {
                    sh """
                    #!/bin/bash
                    ssh -i $SSH_CRED -t -o StrictHostKeyChecking=no ubuntu@54.157.52.76 << EOF
                    curl ifconfig.co/ip
                    df -h
                    exit
                    << EOF
                    """
                }
                
            }
        }
    }
}

