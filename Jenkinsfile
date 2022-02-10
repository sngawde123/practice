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
                try {
                  notifyBuild('STARTED')
                    sh 'mvn clean package'
               
                } catch (e) {
                  currentBuild.result = "Failed"
                  throw e
                } finally {
                  notifyBuild(currentBuild.result)
                }
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
}
