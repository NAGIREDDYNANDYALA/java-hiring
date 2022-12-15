pipeline {
    agent any

    stages {
        stage('Git Checkout') {
            steps {
                git branch: 'main', credentialsId: 'siva-credentials', url: 'https://github.com/NAGIREDDYNANDYALA/java-hiring'
            }
        }
        
         stage('Maven Build') {
            steps {
                sh "mvn clean package"
            }
        }
        
        stage('Tomcat Deploy') {
            steps {
                sshagent(['tomcat-creds']) {
                     sh "scp -o StrictHostKeyChecking=no target/*.war ec2-user@172.31.44.228:/opt/tomcat9/webapps"
                     sh "ssh ec2-user@172.31.44.228 /opt/tomcat9/bin/shutdown.sh"
                     sh "ssh ec2-user@172.31.44.228 /opt/tomcat9/bin/startup.sh"
                }
            }
        }
    }
}
