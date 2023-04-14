pipeline {
    agent any

    stages {
        stage('Maven Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage("Dev Deploy"){
            steps{
              sshagent(['tocat-dev']) {
                  // copy war file into tomcat sever
                  sh "scp -o StrictHostKeyChecking=no target/*.war ec2-user@18.222.186.231:/opt/tomcat9/webapps/"
                  sh "ssh ec2-user@18.222.186.231 /opt/tomcat9/bin/shutdown.sh"
                  sh "ssh ec2-user@18.222.186.231 /opt/tomcat9/bin/startup.sh"
              }
            }
        }
    }
}

