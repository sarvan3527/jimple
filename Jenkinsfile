// pipeline {
//     agent any
//     stages {
//         stage('Build') {
//             steps {
//                 // Your build commands here
//             }
//         }
//         stage('Test') {
//             steps {
//                 // Your testing commands here
//             }
//         }
//         stage('Deploy') {
//             steps {
//                 // Your deployment commands here
//             }
//         }
//     }
// }


pipeline{
    agent any
    options{
        buildDiscarder(logRotator(numToKeepStr: '5', daysToKeepStr: '5'))
        timestamps()
    }
    environment{

        registry = "<dockerhub-username>/<repo-name>"
        registryCredential = '<dockerhub-credential-name>'
    }

    stages{
       stage('Building image') {
      steps{
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }
       stage('Deploy Image') {
      steps{
         script {
            docker.withRegistry( '', registryCredential ) {
            dockerImage.push()
          }
        }
      }
    }
}