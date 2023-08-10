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

        registry = "sarvan3527/my-app"
        registryCredential = '9ce2e490-4fcc-4dd1-a7ff-7e57a56148e7'
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
}
