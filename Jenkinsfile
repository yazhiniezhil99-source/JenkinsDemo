pipeline {
    agent any

    triggers {
        pollSCM('H/1 * * * *')
    }

    stages {
        stage('Build Java') {
            steps {
                echo 'Building Java project...'
                bat 'javac Hello.java'
            }
        }

        stage('Test Java') {
            steps {
                echo 'Testing Java project...'
                bat 'java Hello'
            }
        }

        stage('Deploy Website to AWS') {
            steps {
                withCredentials([sshUserPrivateKey(
                    credentialsId: 'aws-ssh-key',
                    keyFileVariable: 'SSH_KEY'
                )]) {
                    bat '''
                    "C:\\Windows\\System32\\OpenSSH\\scp.exe" -i "%SSH_KEY%" -o StrictHostKeyChecking=no Dockerfile index.html ec2-user@13.60.97.36:~/JenkinsDemo/

                    "C:\\Windows\\System32\\OpenSSH\\ssh.exe" -i "%SSH_KEY%" -o StrictHostKeyChecking=no ec2-user@13.60.97.36 "cd ~/JenkinsDemo && docker build -t yazhini-website . && docker rm -f yazhini-website-container || true"

                    "C:\\Windows\\System32\\OpenSSH\\ssh.exe" -i "%SSH_KEY%" -o StrictHostKeyChecking=no ec2-user@13.60.97.36 "docker run -d --restart unless-stopped --name yazhini-website-container -p 80:80 yazhini-website"
                    '''
                }
            }
        }
    }
}