node {
    
   def mvnHome
   stage('Preparation') { // for display purposes
      // Get some code from a GitHub repository
      git credentialsId: 'd0d27bb8-e7e1-4413-be4d-4a6b75d1af62', url: 'https://github.com/sushilgurjar/jenkins_test.git'
      // Get the Maven tool.
      // ** NOTE: This 'M3' Maven tool must be configured
      // **       in the global configuration.           
      mvnHome = tool 'mvn3'
      env.JAVA_HOME="${tool 'jdk8'}"
      env.PATH="${env.JAVA_HOME}/bin:${env.PATH}"
       
      
   }
   stage('Build') {
      // Run the maven build
      if (isUnix()) {
         sh "'${mvnHome}/bin/mvn' -f api-gateway/pom.xml -Dmaven.test.failure.ignore clean package"
          sh "echo my current directory is:"
          sh "pwd" 
      } else {
         bat(/"${mvnHome}\bin\mvn" -Dmaven.test.failure.ignore clean package/)
      }
   }
   stage('Results') {
      junit '**/api-gateway/target/surefire-reports/*.xml'
      archiveArtifacts 'api-gateway/target/*.jar'
   }
}
