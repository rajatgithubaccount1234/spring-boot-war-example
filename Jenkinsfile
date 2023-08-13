pipeline{
    agent {
        label "linux"
    }
     tools {
        maven 'Maven' 
    }

    stages{
        stage("Test"){
            steps{
                 slackSend channel: 'devops', message: 'Job Started'
                sh 'mvn --version'
                sh 'mvn test'
              
                echo "========executing Mvn Test========"
            }
            
        }
        stage("Build"){
            steps{
                 sh 'mvn package'
                echo "========executing mvn Package========"
            }
            
        }
        stage("Deploy on Test"){
            steps{
               deploy adapters: [tomcat9(credentialsId: '9', path: '', url: 'http://192.168.159.130:8080')], contextPath: '/app', war: '**/*.war'
                echo "========executing Deploy on container========"
            }
            
        }
        stage('Continue ') {
            input {
                message "Should we continue?"
                ok "Yes we Should"
            }
            steps {
                deploy adapters: [tomcat9(credentialsId: '9', path: '', url: 'http://192.168.159.129:8080')], contextPath: '/app', war: '**/*.war'
                echo "Deployong on Proddd"
            }
        }    
                
        stage("Deploy  on Prod"){
            steps{
                
                echo "========executing Deploy on Prod========"
            }
            
        }
    }
    post{
        always{
            echo "========always========"
        }
        success{
            slackSend channel: 'devops', message: 'Job Sucess'
            echo "========pipeline executed successfully ========"
        }
        failure{
            slackSend channel: 'devops', message: 'Job Failed'
            echo "========pipeline execution failed========"
        }
    }
}
