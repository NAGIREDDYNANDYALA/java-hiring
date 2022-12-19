pipeline {
    agent any

    stages {
       
         stage('Maven Build') {
             when {
                 branch 'develop'
             }
            steps {
                sh "mvn clean package"
            }
        }
        
        stage('Tomcat Deploy - Dev') {
            when {
                 branch 'develop'
             }
            steps {
                sshagent(['tomcat-creds']) {
                      echo "Deploying into dev"
            }
        }
        stage('Tomcat Deploy - Prod') {
            when {
                 branch 'main'
             }
            steps {
                echo "Deploying into production"
            }
        }
    }
}
}
