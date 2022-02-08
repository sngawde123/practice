pipeline {
    agent any
    environment {
        PATH = "$PATH:/etc/maven/apache-maven-3.8.4/bin"
    }
    stages {
        stage('GetCode') {
            steps {
                echo 'https://github.com/ravdy/javaloginapp.git'
            }
        }
        
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }   
 
        stage("SpnarQube analysis") {
        
            steps {
        withSonarQubeEnv("sonarqube-8.9.2") {
        sh "mvn sonar:sonar"
    }        
        }
        
        }
            
    }
}
