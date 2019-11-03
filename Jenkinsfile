pipeline {

  environment {
    registry = "nevincleetus/java-web-app-cicd"
    registryCredential = 'dockerhub'
  }
  agent any
  stages {

     stage('Docker Build') {
         agent any
         steps {
             sh 'docker build -t nevincleetus/java-web-app-cicd:latest .'
         }
     }
     stage('Docker Run ') {
         agent any
         steps {
             sh 'docker run -itd nevincleetus/java-web-app-cicd:latest '
         }
     }

     stage('Docker Push') {
         agent any
         steps {
              withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'dockerhubPassword', usernameVariable: 'dockerhubUser')]) {
                sh "docker login -u ${env.dockerhubUser} -p ${env.dockerhubPassword}"
                sh 'docker push nevincleetus/java-web-app-cicd:latest'
              }
         }
     }
  }
} 

