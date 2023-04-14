pipeline {
    agent any
	environment {
  	TP = "172.31.35.105"
		
  	TU = "ec2-user"
	}

    stages {
        stage('Maven Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage("Dev Deploy"){
            steps{
              sshagent(['deploy1']) {
                  sh "scp -o StrictHostKeyChecking=no target/*.war $TU@$TP:/opt/tomcat9/webapps/"
                  sh "ssh $TU@$TP /opt/tomcat9/bin/shutdown.sh"
                  sh "ssh $TU@$TP /opt/tomcat9/bin/startup.sh"
              }
            }
        }
    }
}
