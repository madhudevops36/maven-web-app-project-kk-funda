node
{
  echo "git job name : ${env.JOB_NAME}
  echo "Build number is: ${env.BUILD_NUMBER}
  echo "node name is:${env.NODE_NAME}
  properties([buildDiscarder(logRotator(artifactDaysToKeepStr: '5', artifactNumToKeepStr: '5', daysToKeepStr: '5', numToKeepStr: '5')), pipelineTriggers([pollSCM('* * * * *')])])  
   def mavenHome=tool name: "maven-3.9.9"
   stage('checkout')
   {
       git branch: 'airtel-dev', credentialsId: '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', url: 'https://github.com/madhudevops36/maven-web-app-project-kk-funda.git'
   }
   stage('build')
   {
       sh "${mavenHome}/bin/mvn clean package"
   }
   stage('SQ Report')
   {
       sh "${mavenHome}/bin/mvn clean sonar:sonar"
   }
   stage('Upload artifact')
   {
       sh "${mavenHome}/bin/mvn clean deploy"
   }
   stage('Deploy to Tomcat')
   {
      sshagent(['30d02787-8bd0-4b68-b76a-2dee9cb5358b'])
      {
           sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@65.2.127.133:/opt/apache-tomcat-9.0.97/webapps/"

      }
} 
   
}
