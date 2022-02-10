pipeline {
    agent any
        environment {
            PATH = "$PATH:/etc/maven/apache-maven-3.8.4/bin"
        }
    node {
        try {
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
                stage('Email Notifications') {
                    steps {
                        mail bcc: '', body: 'Hello', cc: '', from: '', replyTo: '', subject: 'Jenkins job', to: 'snehalgawde724@gmail.com'
                    }
                }
            }
                echo 'Build Success'
        } catch (err) {
                mail bcc: '', body: '${err}', cc: '', from: '', replyTo: '', subject: 'Failure', to: 'snehalgawde724@gmail.com'
        echo "Failed: ${err}"
        }
    }
}
