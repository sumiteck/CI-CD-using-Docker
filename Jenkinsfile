pipeline {
    agent any
 
   tools
    {
       maven "Maven"
    }
    
    	environment {
		dockerhub=credentials('dockerhub')
	}
 stages {
      stage('checkout') {
           steps {
             
                git branch: 'master', url: 'https://github.com/sumiteck/CI-CD-using-Docker.git'
             
          }
        }
  stage('Execute Maven') {
           steps {
             
                sh 'mvn package'             
          }
        }
stage('Docker Build and Tag') {
           steps {
		  
                   sh 'docker build -t samplewebapp:latest .' 
                sh 'docker tag samplewebapp sumitk68/samplewebapp:latest'
                //sh 'docker tag samplewebapp nikhilnidhi/samplewebapp:$BUILD_NUMBER'
               
          }
        }
     
  stage('Publish image to Docker Hub') {
          
        
            steps {
        withDockerRegistry([ credentialsId: "dockerhub", url: "" ]) {
          sh  'docker push sumitk68/samplewebapp:latest'
        //  sh  'docker push nikhilnidhi/samplewebapp:$BUILD_NUMBER' 
        }
                  
          }
  }
        
     
      stage('Run Docker container on Jenkins Agent') {
             
            steps 
   {
                sh "docker run -d -p 8003:8080 sumitk68/samplewebapp"
 
            }
        }

    }
 }
    
