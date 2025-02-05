pipeline {
 agent any
 
 tools {
   jdk 'jdk17'
   maven '3.9.9'
 }
   stages{
     stage('checkout') {
       steps {
          checkout scm
       }
     }
     stage('build') {
       steps {
          sh "mvn clean install -DskipTests"
       }
     }
       stage('Deploy') {
           steps {
            withCredentials([usernamePassword(credentialsId: 'jenkins', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
    // Check if the WAR file exists before attempting the copy
    sh 'ls -al /var/lib/jenkins/workspaceCI-CD/target/'

    // Only proceed if the file exists
    sh 'echo $PASS | sudo -S cp /var/lib/jenkins/workspace/CI-CD/target/webapps.war /opt/tomcat/webapps'

           }
          }
       }
    
        stage('test') {
          steps {
           echo "testing..."
          }
        }
       }
     }
