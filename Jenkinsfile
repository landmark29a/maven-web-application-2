pipeline{
  agent any
 tools {
   maven "maven3.8.6"
}
 stages{
   stage( '1cloning' ){
       steps{
         sh "echo 'cloning the latest application version' "
         git branch: 'feature', credentialsId: 'github', url: 'https://github.com/landmark29a/maven-web-application-2'
  }
}
   stage( '2testing+build' ){
     steps{ 
        sh "echo 'running Junit test cases' "
        sh "echo 'testing must passed to create artifacts' "
        sh "mvn clean package"
    }
   }
   stage( '4codeQuality' ){
     steps{
      sh "echo 'performingcodeQuality' "
      sh "mvn sonar:sonar"
     }
   }
   stage( '5uploadArtifact' ){
       steps{
         sh "echo 'uploading2nexus' "
         sh "mvn deploy"
       }
     }
   //stage( '6deploy2uat' ){}
   //stage( '7approvalGate' ){}
   stage( '8deploy2prod' ){
     steps{
    deploy adapters: [tomcat8(credentialsId: 'tomcat-credentials', path: '', url: 'http://44.201.181.117:8091/')], contextPath: null, war: 'target/*war'
     }
   }
 }
   /*stage( '9 notification' ){}
}
 //options{}
 post{
    success{     
emailext body: '''hey guys, good job, build and deployment is successfull

thanks,

landmark
+''', subject: 'success', to: 'claudia.temdenou@gmail.com'

}
    failure{}
    always{}
}
*/
}
