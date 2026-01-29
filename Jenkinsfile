pipeline {
    agent any
    
    tools {
        maven 'Maven' 
    }
    
    stages {
        stage("Test") {
            steps {
                sh "mvn test"
            }
        }
        
        stage("Build") {
            steps {
                sh "mvn package"
            }
        }
        
        stage("Deploy on Test") {
            steps {
                // Using Deploy to container plugin
                deploy adapters: [tomcat9(
                    alternativeDeploymentContext: '', 
                    credentialsId: 'tomcat', 
                    path: '', 
                    url: 'http://10.0.2.15:8080'
                )], 
                contextPath: '/app', 
                war: '**/*.war'
            }
        }
    }
    
    post {
        always {
            echo "========always========"
        }
        success {
            echo "========pipeline executed successfully ========"
        }
        failure {
            echo "========pipeline execution failed========"
        }
    }
}
