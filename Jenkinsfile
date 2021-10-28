pipeline {
    agent any
 stages {
  stage('Docker Build and Tag') {
           steps {
              
                sh 'docker build -t nginxtest:latest .' 
                  sh 'docker tag nginxtest nikhilnidhi/nginxtest:latest'
                sh 'docker tag nginxtest nikhilnidhi/nginxtest:$BUILD_NUMBER'
               
          }
        }
     
  stage('Publish image to Docker Hub') {
          
            steps {
        withDockerRegistry([ credentialsId: "dockerHub", url: "" ]) {
          sh  'docker push nikhilnidhi/nginxtest:latest'
          sh  'docker push nikhilnidhi/nginxtest:$BUILD_NUMBER' 
        }
                  
          }
        }
     
      stage('Run Docker container on Jenkins Agent') {
             
            steps {
                sh "docker run -d -p 4030:80 nikhilnidhi/nginxtest"
 
            }
        }
 stage('Run Docker container on remote hosts') {
             
            steps {
                sh "docker -H ssh://jenkins@15.206.172.149 run -d -p 4001:80 nikhilnidhi/nginxtest"
 
            }
        }
    }
}
