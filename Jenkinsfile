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
                        sh "sshpass -p '$USERPASS' -v ssh -o StrictHostKeyChecking=no -p 23 $USERNAME@$prod_ip \"docker pull ypasmk/robot-framework\""
                        try {
                            sh "sshpass -p '$USERPASS' -v ssh -o StrictHostKeyChecking=no -p 23 $USERNAME@$prod_ip \"docker stop ypasmk/robot-framework\""
                            sh "sshpass -p '$USERPASS' -v ssh -o StrictHostKeyChecking=no -p 23 $USERNAME@$prod_ip \"docker rm ypasmk/robot-framework\""
                        } catch (err) {
                            echo: 'caught error: $err'
                        }
                        sh "sshpass -p '$USERPASS' -v ssh -o StrictHostKeyChecking=no $USERNAME@$prod_ip \"docker run --restart always --name train-schedule -p 8080:8080 -d guru4tech/train-schedule:${env.BUILD_NUMBER}\""
                    }
                }
            }
        }
    }
}
