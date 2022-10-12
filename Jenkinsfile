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
                    chown -R ubuntu ~/.ssh/Devops.pem
                    chmod 700 ~/.ssh/Devops.pem
                    chmod 600 ~/.ssh/Devops.pem
                    ssh -i $SSH_CRED -t -o StrictHostKeyChecking=no ubuntu@54.197.15.121 << EOF
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

