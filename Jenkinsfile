node{
     
    stage('SCM Checkout'){
        git url: 'https://github.com/praju7090/praveen.git'
    }
    
stage('Compile-Package'){

      def mvnHome =  tool name: 'Maven-3.5.6"', type: 'maven'   
      sh "${mvnHome}/bin/mvn clean package"
	  sh 'mv target/myweb*.war target/newapp.war'
   }
   
   stage('Build Docker Imager'){
   sh 'docker build -t praveen7090/java-web-app .'
   }
   stage('Docker Image Push'){
   withCredentials([string(credentialsId: 'Docker_Hub_Pwd', variable: 'Docker_Hub_Pwd')]) {
   sh "docker login -u praveen7090 -p ${Docker_Hub_Pwd}"
    }
   sh 'docker push praveen7090/java-web-app'
   }
  
   stage('Docker deployment'){
   sh 'docker run -d -p 8090:8080 --name tomcattest praveen7090/java-web-app' 
   }
}

