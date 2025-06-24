
  node
{
def mavenHome=tool name: "maven-3.9.9"
stage('checkout')
{
git branch: 'airtel-dev', credentialsId: 'bf09f2bb-5193-494f-9bfd-ac740eca8c92', url: 'https://github.com/madhudevops36/maven-web-app-project-kk-funda.git'
}
stage('buid')
{
    sh "${mavenHome}/bin/mvn clean package"
}
stage('sonarqube report')
{
    sh "${mavenHome}/bin/mvn clean sonar:sonar"
}
stage('nexus')
{
   sh "${mavenHome}/bin/mvn clean deploy"
}
stage('Tomcat Deploy')
{
sshagent(['474c7568-3831-4397-8375-88a7bcc254a3'])
   {
  
        sh 'scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@65.0.180.19:/opt/apache-tomcat-9.0.106/webapps/'
    }
}

     }
