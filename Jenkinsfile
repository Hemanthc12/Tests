pipeline {
    agent any
	environment {
  	TP = "172.31.41.0"
  	TU = "ec2-user"
	}

    stages {
        stage('Maven Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        
    }
	post {
  	failure {
    echo "Job failed, sending failuer email".
  	}
    }
}
