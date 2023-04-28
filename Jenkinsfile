pipeline{
     tools {
        maven 'Maven' 
    }
    agent any

    stages{
        stage("Test"){
            steps{
                // mvn test
                sh "mvn test"
                echo "========executing A========"
            }
            
            
        }
        stage("Build"){
            steps{
                sh "mvn package"
                echo "========executing A========"
            }
            
            
        }
        stage("Deploy on Test"){
            steps{
                // deploy on container -> plugin
                deploy adapters: [tomcat9(credentialsId: 'tomcat', path: '', url: 'http://3.110.30.154:8080')], contextPath: '/app', war: '**/*.war'
                echo "========executing A========"
            }
            
            
        }
        stage("Deploy on Prod"){
            steps{
                  // deploy on container -> plugin
                  deploy adapters: [tomcat9(credentialsId: 'tomcat', path: '', url: 'http://35.154.8.73/:8080')], contextPath: '/app', war: '**/*.war'
                                  echo "========executing A========"
            }
            
        }
    }
    post{
        always{
            echo "========always========"
        }
        success{
            echo "========pipeline executed successfully ========"
        }
        failure{
            echo "========pipeline execution failed========"
        }
    }
}
