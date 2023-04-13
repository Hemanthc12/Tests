pipeline {
    agent any

    stages {
        stage('Git Checkout') {
            steps {
                git branch: 'main', credentialsId: 'github', url: 'https://github.com/Hemanthc12/Tests.git'
            }
        }
        stage('Maven Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage("Dev Deploy"){
            steps{
              sshagent(['tocat-dev']) {
                  // copy war file into tomcat sever
                  sh "scp -o StrictHostKeyChecking=no target/*.war ec2-user@172.31.41.0:/opt/tomcat9/webapps/"
                  sh "ssh ec2-user@172.31.41.0 /opt/tomcat9/bin/shutdown.sh"
                  sh "ssh ec2-user@172.31.41.0 /opt/tomcat9/bin/startup.sh"
              }
            }
        }
    }
}

