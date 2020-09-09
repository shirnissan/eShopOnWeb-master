pipeline {
  environment {
    registry = "shirnissan/eshoponweb"
    registryCredential = 'docker-creds'
  }
	agent any
   stages {
	         stage('folder check') {
         steps {
            sh "pwd"
	    sh "ls"
         }
      }
	stage('Docker ps') {
          steps {
            sh "Docker ps"
         }
      }
      stage('Docker build') {
         steps {
            sh "docker-compose up -d --build"
	    sh "docker-compose build -t shirnissan/eshoponweb:${BUILD_NUMBER} ."
         }
      }
      stage('Login to docker hub') {
         steps {
   		script {
          		docker.withRegistry( '', registryCredential ) 
         	}         
	}
      }
      stage('Docker push') {
         steps {
           sh "docker push  shirnissan/eshoponweb:${BUILD_NUMBER}"
         }
      }
      stage('Docker run') {
         steps {
           sh " docker run -d -p 8080:80 --name myapp shirnissan/eshoponweb:${BUILD_NUMBER}"
         }
      }
   } 
    post {
        always {
            cleanWs deleteDirs: true, notFailBuild: true
        }
    }
}
