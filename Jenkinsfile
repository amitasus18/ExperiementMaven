pipeline{
    agent any
    tools{
        jdk 'JAVA_HOME'
        maven 'mymaven'
    }
    stages{
        stage('Compile'){        
            steps{
                script{
                    echo "Building the code"
                    sh 'mvn compile'
                 }   
                }
            }
        
        stage('Test'){
         steps {
            script{
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
        steps{
          script{
            echo "Package the app"
            sh 'mvn package'
                    }
            }
        }
    }
}
