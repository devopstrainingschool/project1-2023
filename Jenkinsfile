pipeline {
  agent any
  tools { 
    maven "project1"
  }
  environment {
        
        IMAGE_TAG = "${BUILD_NUMBER}"
   
  }
  
  stages {
    stage ("maven Clean") {
      steps {
        sh 'mvn clean'
      }
      
    }
    
    stage ("maven package") {
      steps {
        sh 'mvn package'
      }
      
    }
  
  
  
  
  }



}
