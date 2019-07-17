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
                    }
                }
            }
        }
    }
}
