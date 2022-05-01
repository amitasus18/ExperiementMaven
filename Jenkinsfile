pipeline{
    agent none
    tools{
        jdk 'JAVA_HOME'
        maven 'mymaven'
    }
    environment{
        TEST_SERVER_IP='ec2-user@172.31.28.36'
    }
    stages{
        stage('Compile'){   
            agent any     
            steps{
                script{
                    echo "Building the code"
                    sh 'mvn compile'
                 }   
                }
            }
        
        stage('Test'){
            agent any
         steps {
            script{
                sshagent(['TEST_SERVER']){
                    echo "Testing the code"
                    sh "scp -o StrictHostKeyChecking=no server-script.sh ${TEST_SERVER_IP}:/home/ec2-user"
                    sh "ssh -o StrictHostKeyChecking=no ${TEST_SERVER_IP} 'bash ~/server-script.sh' "
                    sh 'mvn test'
                }
                echo "Testing the Code"
                sh 'mvn test'
            }
        }
        post {
            always{
                junit 'target/surefire-reports/*.xml'
            }
        }
        }
        stage('PACKAGE'){
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
