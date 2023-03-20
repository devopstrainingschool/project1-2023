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
        sh 'docker build -t devopstrainingschool/project1-2023:${BUILD_NUMBER} .'
      }
      
    }
    stage ("Docker push to dockerhub") {
      steps {
        withDockerRegistry([ credentialsId: "docker_creds" , url: "https://index.docker.io/v1/" ]){
          sh 'docker push devopstrainingschool/project1-2023:${BUILD_NUMBER}'
        }
      
    }
      
      }
    stage('Github clone the project1-2023-deployment'){
            steps {
                script{
                  catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
              sh "rm -rf project1-2023-deployment"       
              sh "git clone https://github.com/devopstrainingschool/project1-2023-deployment.git"
              
            
             
                    }
                  }
                }
            }
        }
  
    stage('Make yaml files changes & push them to Github'){
            steps {
                script{
                  catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    
                     sh """
                    git config --global user.name "devopstrainingschool"
                    git config --global user.email "devopstrainingschool@gmail.com" """
                    withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                      dir("project1-2023-deployment"){
                        sh "pwd"
                        sh "echo $BUILD_NUMBER"
                        sh "cat my-app.yaml"
                        sh "sed -i -e 's+devopstrainingschool/project1-2023.*+devopstrainingschool/project1-2023:${env.BUILD_NUMBER}+g'  my-app.yaml"
                        sh "cat my-app.yaml"
                        sh " git add ."
                        sh " git commit -m 'Updated the deployment file'"
                        sh "git push http://$GIT_USERNAME:$GIT_PASSWORD@github.com/devopstrainingschool/project1-2023-deployment.git master"
                      }
                      
             
                    }
                  }
                }
            }
        }
    

    
    
  
  }



}
