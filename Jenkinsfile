properties([parameters([string(description: 'Enter recipient email address', name: 'Recipient_IDs'), booleanParam(description: 'Email', name: 'Email_Enable')])])
pipeline {
    agent any
    environment {
        PATH = "$PATH:/etc/maven/apache-maven-3.8.4/bin"
    }
    stages {
        stage("list env vars") {
            steps {
                sh "printenv | sort"
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
    }
    post {
        success {
            script{
                emailBody = "Hi Sender,\nThis is an autogenerated email.\nBuild URL: ${env.BUILD_URL}\nBuild Number: ${env.BUILD_NUMBER}\nJob Name: ${env.JOB_NAME}\nThanks,\nDevOps Team"
                emailext attachLog: true, 
                body: emailBody, 
                subject: "Build Status : ${currentBuild.result} || Pipeline Details: ${currentBuild.fullDisplayName}", 
                to: "${params.Recipient_IDs}"
                mimeType: 'text/html'
            }
        }
        failure {
            script {
                emailBody = "Hi Sender,\nThis is an autogenerated email.\nBuild URL: ${env.BUILD_URL}\nBuild Number: ${env.BUILD_NUMBER}\nJob Name: ${env.JOB_NAME}\nThanks,\nDevOps Team"
                emailext attachLog: true, 
                body: emailBody, 
                subject: "Build Status : ${currentBuild.result} || Pipeline Details: ${currentBuild.fullDisplayName}", 
                to: "${params.Recipient_IDs}"
                mimeType: 'text/html'
            }
        }
        
    }
}
