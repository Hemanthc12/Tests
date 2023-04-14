pipeline {
    agent any


    parameters {
        string defaultValue: 'main', description: 'chose the branch', name: 'BN'
        }


        environment {
            TP = "172.31.35.105"
            TU = "ec2-user"
            }


        stages {
            stage('Git Checkout') {
                    
                    steps {
                        git branch: "${params.BN}", credentialsId: 'github', url: 'https://github.com/Hemanthc12/Tests.git'
                    }
                }


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
         post {
            success {
                echo 'build is successful'
            }
            failure {
                echo 'build is failed'
            }
        }


}
