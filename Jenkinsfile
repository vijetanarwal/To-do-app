pipeline {
    agent any
    tools{
        maven 'maven'
    }
    stages {
        stage('Build') {
            steps {
                bat 'mvn clean package'
            }
            post {
                success{
                    echo 'Archiving the Artifacts'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
        stage('Deploy to tomcat server') {
            steps {
                deploy adapters: [tomcat9(credentialsId: 'tomcat', path: '', url: 'http://localhost:9090/')], contextPath: null, war: '**/*.war'
            }
        }
    }
}