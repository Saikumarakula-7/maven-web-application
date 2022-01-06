node{

def mavenHome = tool name : "maven 3.8.4"

stage('checkout code'){
git branch: 'development', credentialsId: 'Github', url: 'https://github.com/Saikumarakula-7/maven-web-application.git'
}

stage('build'){
  sh "${mavenHome}/bin/mvn clean package"
}

stage('sonarqube report'){
 sh "${mavenHome}/bin/mvn clean sonar:sonar"
}

stage('upload artifacts to nexus'){
sh "${mavenHome}/bin/mvn clean deploy"
}
stage('deploy to tomcat'){
sshagent(['c47b6f59-6947-43ba-9959-212c168452dc']) {
   sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@65.2.79.1:/opt/apache-tomcat-9.0.56/webapps"
}
    
}
}
