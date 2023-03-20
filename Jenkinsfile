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
   stage ("Docker build") {
      steps {
        sh 'docker build -t devopstrainingschool/project1-2023:IMAGE_TAG .'
      }
      
    }
  
  
  
  }



}
