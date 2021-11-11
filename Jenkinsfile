pipeline{
    agent any
    environment{
        dockerImage = ''
        registry = "71098/whiteboard-app"
        registryCredential = 'docker_hub'
    }
    stages {
        stage('checkout'){
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/vipul71098/whiteboard.git']]])
            }
        }
        stage('Build Docker image') {
            steps {
                script {
                    dockerImage = docker.build registry
                }
            }
        }
    
        stage('docker stop container') {
         steps {
            sh 'docker ps -f name=mywhiteboard -q | xargs --no-run-if-empty docker container stop'
            sh 'docker container ls -a -fname=mywhiteboard -q | xargs -r docker container rm'
         }
       }
        
        stage('Docker Run') {
           steps{
               script {
                 dockerImage.run("-p 8096:5000 --rm --name mywhiteboard")
               }
            }
       }
        
    }
}
