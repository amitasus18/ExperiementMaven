pipeline{
    agent none
    tools{
        jdk 'JAVA_HOME'
        maven 'mymaven'
    }
    environment{
        TEST_SERVER_IP='ec2-user@18.118.19.21'
    }
    stages{
        stage('MPDP-Compile'){   
            agent any     
            steps{
                script{
                    echo "MPDP - Building the code"
                    sh 'mvn compile'
                 }   
                }
            }
        
        stage('MPDP-Test'){
            agent any
         steps {
            script{
                sshagent(['Test_Server']){
                    echo "Testing the code"
                    sh "scp -o StrictHostKeyChecking=no server-script.sh ${TEST_SERVER_IP}:/home/ec2-user"
                    sh "ssh -o StrictHostKeyChecking=no ${TEST_SERVER_IP} 'bash ~/server-script.sh' "
                    sh 'mvn test'
                }
                }
        }
        post {
            always{
                junit 'target/surefire-reports/*.xml'
            }
        }
        }
        stage('MPDP-PACKAGE'){
            agent {label 'Test-Server'}
        steps{
          script{
            echo "Package the app"
            sh 'mvn package'
                    }
            }
        }
    }
}
