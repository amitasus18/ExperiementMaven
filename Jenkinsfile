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
                    sh 'mvn complile'
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
