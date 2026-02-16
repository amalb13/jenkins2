pipeline {
    agent any
    tools {
        maven 'maven'
        jdk 'jdk21'
    }
    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/amalb13/jenkins2'
            }
        }
        stage('Build with Maven') {
            steps {
                dir('my-webapp') {
                    bat 'mvn clean package'
                }
            }
        }
        stage('Deploy to Tomcat') {
            steps {
                dir('my-webapp') {
                    deploy adapters: [tomcat9(credentialsId: 'tomcat-creds', path: '', url: 'http://localhost:8081')],
                           contextPath: 'my-webapp',
                           war: 'target/my-webapp.war'
                }
            }
        }
    }
}
