pipeline {
    agent any 
    environment {
        //once you sign up for Docker hub, use that user_id here
        registry = "sarvan3527/mypythonapp2"
        //- update your credentials ID after creating credentials for connecting to Docker Hub
        registryCredential = '9ce2e490-4fcc-4dd1-a7ff-7e57a56148e7'
        dockerImage = ''
    }
    
    stages {
        stage('Cloning Git') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: '', url: 'https://github.com/sarvan3527/j-implemen.git']]])       
            }
        }
    
    // Building Docker images
    stage('Building image') {
      steps{
        script {
          dockerImage = docker.build registry
        }
      }
    }
    
     // Uploading Docker images into Docker Hub
    stage('Upload Image') {
     steps{    
         script {
            docker.withRegistry( '', registryCredential ) {
            dockerImage.push()
            }
        }
      }
      
    }
    stage('Docker Run') {
        steps{
            script {
                bat "docker run %registry%"
            }
        }
    }
    
  }
}
 	
