pipeline {
    agent any
    
    parameters {  
        choice(name: 'ENV', choices: ['QA', 'UAT'], description: 'Pick Env value')
    }
    
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        
        stage('Build') {
            steps {
                sh '/home/shivani/Documents/devops/apache-maven-3.9.6/bin/mvn install'
            }
        }
        
        stage('Deployment') {
            steps {
                script {
                    if (env.ENV == 'QA') {
                        sh 'cp target/green1.war /home/shivani/Documents/devops/apache-tomcat-9.0.88/webapps'
                        echo "Deployment has been done on QA!"
                    } else if (env.ENV == 'UAT') {
                        sh 'cp target/green1.war /home/shivani/Documents/devops/apache-tomcat-9.0.88/webapps'
                        echo "Deployment has been done on UAT!"
                    }
                    stage('Slack') {
                        steps {
                            slackSend baseUrl: 'https://hooks.slack.com/services/', botUser: true, channel: 'green1', color: 'good', message: 'hello green1', notifyCommitters: true, teamDomain: 'devops', tokenCredentialId: 'green1', username: 'green1'
                }
            }
        }
    }
}
