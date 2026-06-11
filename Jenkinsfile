node
{

   def mavenHome= tool name: "maven-test"
   stage('git checkout')
   {
      git branch: 'master', url: 'https://github.com/shashi155365/maven-webapplication-project-kkfunda.git'
   }
   stage('COMPILE')
   {
    sh  "${mavenHome}/bin/mvn compile" 
   }
   stage('SQ REPORT')
   {
        sh  "${mavenHome}/bin/mvn sonar:sonar" 
   }
   stage('Build')
   {
     sh  "${mavenHome}/bin/mvn package"
   }
   stage('Deploy to Nexus')
   {
      sh  "${mavenHome}/bin/mvn deploy"
   }

   stage('Deploy to Tomcat') 
    {
      
      sh """

      curl -u kk:password \
--upload-file /var/lib/jenkins/workspace/New-scriptedway-pipeline/target/maven-web-application.war \
"http://3.110.51.91:8080/manager/text/deploy?path=/maven-web-application&update=true"
          
        """
    }
	
}
