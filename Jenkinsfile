pipeline {
  agent any
    tools {
      maven 'maven'
                 jdk 'java1.8'
    }
    stages {      
        stage('Build maven') {
            steps { 
                    sh 'pwd'      
                    sh 'mvn  clean install package'
            }
        }
        
        stage('Copy Artifact') {
           steps { 
                   sh 'pwd'
		   sh 'cp -r target/*.jar docker'
           }
        }
         
        stage('Build docker image') {
           steps {
               script {         
                 withCredentials([usernamePassword( credentialsId: 'dockerhub', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                 docker.withRegistry('', 'dockerhub') {
                 sh "docker login -u ${USERNAME} -p ${PASSWORD}"
                 customImage.push("${env.BUILD_NUMBER}")
}
                 }                     
           }
        }
	  }
    }
}
