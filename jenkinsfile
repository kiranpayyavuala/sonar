node{
   stage('SCM Checkout'){
     git 'https://github.com/kiranpayyavuala/sonar.git'
   }
   stage('Compile-Package'){
      // Get maven home path
      def mvnHome =  tool name: 'MAVEN_HOME', type: 'maven'   
      sh "${mvnHome}/bin/mvn package"
   }
   
   stage('SonarQube Analysis') {
        def mvnHome =  tool name: 'MAVEN_HOME', type: 'maven'
        withSonarQubeEnv('sonar') { 
          sh "${mvnHome}/bin/mvn sonar:sonar"
        }
    }
}
