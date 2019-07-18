pipeline {
    agent any
    stages {
       
        stage('DeployToProduction') {
            when {
                branch 'master'
            }
            steps {
                input 'Deploy to Production?'
                milestone(1)
                withCredentials([usernamePassword(credentialsId: 'webserver_login', usernameVariable: 'USERNAME', passwordVariable: 'USERPASS')]) {
                    script {
                        /*sh "sshpass -p '$USERPASS' -v ssh -o StrictHostKeyChecking=no -p 23 $USERNAME@$prod_ip \"docker pull ypasmk/robot-framework\""*/
                        sh "sshpass -p '$USERPASS' -v ssh -o StrictHostKeyChecking=no -p 23 $USERNAME@$prod_ip \"docker run --rm -e USERNAME="Test User" --net=host -v "$PWD/output":/output -v "$PWD/suites":/suites -v "$PWD/scripts":/scripts -v "$PWD/reports":/reports --security-opt seccomp:unconfined --shm-size "256M" ypasmk/robot-framework\""
                    }
                }
            }
        }
    }
}
