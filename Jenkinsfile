pipeline {
    agent any
    environment {
        PATH = "$PATH:/etc/maven/apache-maven-3.8.6/bin"
    }
    stages {
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
                    color = (currentBuild.result == "SUCCESS") ? "Green" : "Red"
                    fullDisplayName = "${currentBuild.fullDisplayName}"
                    result = "${currentBuild.result}"
                    buildUrl = "${env.BUILD_URL}"
                    buildNumber = "${currentBuild.number}"
                    htmlBodyHead = '''<!DOCTYPE html><html><title>Build Notification</title><head><meta name="viewport" content="width=500, initial-scale=1"></head>'''
                    htmlBody = '''<body><div class="card" style="width: 95%;text-align: center;border: 4px solid ''' + color +'''">  
                                        <div class="alert alert-success" style="text-align: center;color: ''' + color + '''"><h1>''' + result + '''</h1></div>
                                        <div class="container">
                                        <h2>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Pipeline Details: ''' + fullDisplayName + '''</h2>
                                        <h2>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Build Number: ''' + buildNumber + '''</h2>
                                        <h2>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<a href="''' + buildUrl + '''" style="background-color: ''' + color +''';color: white;border: 2px solid ''' + color + ''';padding: 10px 20px;text-align: center;text-decoration: none;display: inline-block;">Click here for the Build Logs</a></h2></div></div></body></html>'''
                    emailext attachLog: true, 
                    body: htmlBodyHead + htmlBody,
                    subject: "Build Status : ${currentBuild.number} || Pipeline Details: ${currentBuild.fullDisplayName}", 
                    to: "snehalgawde724@gmail.com",
                    mimeType: 'text/html'
                
            }
        }
        failure {
            script {
               
                    color = (currentBuild.result == "SUCCESS") ? "Green" : "Red"
                    fullDisplayName = "${currentBuild.fullDisplayName}"
                    result = "${currentBuild.result}"
                    buildUrl = "${env.BUILD_URL}"
                    buildNumber = "${currentBuild.number}"
                    htmlBodyHead = '''<!DOCTYPE html><html><title>Build Notification</title><head><meta name="viewport" content="width=500, initial-scale=1"></head>'''
                    htmlBody = '''<body><div class="card" style="width: 95%;text-align: center;border: 4px solid ''' + color +'''">  
                                        <div class="alert alert-failure" style="text-align: center;color: ''' + color + '''"><h1>''' + result + '''</h1></div>
                                        <div class="container">
                                        <h2>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Pipeline Details: ''' + fullDisplayName + '''</h2>
                                        <h2>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Build Number: ''' + buildNumber + '''</h2>
                                        <h2>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<a href="''' + buildUrl + '''" style="background-color: ''' + color +''';color: white;border: 2px solid ''' + color + ''';padding: 10px 20px;text-align: center;text-decoration: none;display: inline-block;">Click here for the Build Logs</a></h2></div></div></body></html>'''
                    emailext attachLog: true, 
                    body: htmlBodyHead + htmlBody,
                    subject: "Current Build Status : ${currentBuild.result} || Pipeline Details: ${currentBuild.fullDisplayName}",
                    to: "snehalgawde724@gmail.com",
                    mimeType: 'text/html'
               
            }
        }
        aborted {
            script {
              
                    color = (currentBuild.result == "SUCCESS") ? "Green" : "Red"
                    fullDisplayName = "${currentBuild.fullDisplayName}"
                    result = "${currentBuild.result}"
                    buildUrl = "${env.BUILD_URL}"
                    buildNumber = "${currentBuild.number}"
                    htmlBodyHead = '''<!DOCTYPE html><html><title>Build Notification</title><head><meta name="viewport" content="width=500, initial-scale=1"></head>'''
                    htmlBody = '''<body><div class="card" style="width: 95%;text-align: center;border: 4px solid ''' + color +'''">  
                                        <div class="alert alert-failure" style="text-align: center;color: ''' + color + '''"><h1>''' + result + '''</h1></div>
                                        <div class="container">
                                        <h2>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Pipeline Details: ''' + fullDisplayName + '''</h2>
                                        <h2>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Build Number: ''' + buildNumber + '''</h2>
                                        <h2>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<a href="''' + buildUrl + '''" style="background-color: ''' + color +''';color: white;border: 2px solid ''' + color + ''';padding: 10px 20px;text-align: center;text-decoration: none;display: inline-block;">Click here for the Build Logs</a></h2></div></div></body></html>'''
                    emailext attachLog: true, 
                    body: htmlBodyHead + htmlBody,
                    subject: "Build Status : ${currentBuild.result} || Pipeline Details: ${currentBuild.fullDisplayName}",
                    to: "snehalgawde724@gmail.com",
                    mimeType: 'text/html'
              
            }
        }   
    }
}   
