pipeline {
    agent any
        environment {
            PATH = "$PATH:/etc/maven/apache-maven-3.8.4/bin"
        }
        stages {
            stage('GetCode') {
                steps {
                    git 'https://github.com/ravdy/javaloginapp.git'
                }
            }
            stage('Build') {
      
                steps {
                script {
             
                    sh 'mvn clean package'
                     
            }
            }
            }
            stage("SpnarQube analysis") {

            steps {
            withSonarQubeEnv("sonarqube-8.9.2") {
            sh "mvn sonar:sonar"
        }        
            }
            }
            stage('Email Notifications') {
                    steps {
                            mail bcc: '', body: 'Hello', cc: '', from: '', replyTo: '', subject: 'Jenkins job', to: 'snehalgawde724@gmail.com'
                }
            }
                
        }
    post {
        success{script{mail bcc: '', body: 'Job is successful', cc: '', from: '', replyTo: '', subject: 'Build Success', to: 'snehalgawde724@gmail.com'}}
        failure{ script{mail bcc: '', body: 'Job is failed', cc: '', from: '', replyTo: '', subject: 'Build Failed', to: 'snehalgawde724@gmail.com'}}
        
    }
}
