pipeline{
    agent any
    environment{
        dockerImage = ''
        registry = "745801/mytestapp"
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
        
        stage('Docker Run') {
           steps{
               script {
                 dockerImage.run("-p 8096:5000 --rm --name mywhiteboard")
               }
            }
       }
        
    }
}
