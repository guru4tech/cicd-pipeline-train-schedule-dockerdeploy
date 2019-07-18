pipeline {
    agent any
    stages {
       
        stage('ExecuteTests') {
            when {
                branch 'master'
            }
            steps {
                input 'Deploy to Production?'
                milestone(1)
                withCredentials([usernamePassword(credentialsId: 'webserver_login', usernameVariable: 'USERNAME', passwordVariable: 'USERPASS')]) {
                    script {
                        /*sh "sshpass -p '$USERPASS' -v ssh -o StrictHostKeyChecking=no -p 23 $USERNAME@$prod_ip \"docker pull ypasmk/robot-framework\""*/
                        sh "sshpass -p '$USERPASS' -v ssh -o StrictHostKeyChecking=no -p 23 $USERNAME@$prod_ip \"docker run --rm -e USERNAME='Test User' --net=host -v '/root/robot-framework-docker/output':/output -v '/root/robot-framework-docker/suites':/suites -v '/root/robot-framework-docker/scripts':/scripts -v '/root/robot-framework-docker/reports':/reports --security-opt seccomp:unconfined --shm-size '256M' ypasmk/robot-framework\""
                    }
                }
            }
        }
    }
}
