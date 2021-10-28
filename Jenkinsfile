pipeline{

	agent any

	environment {
		DOCKERHUB_CREDENTIALS=credentials('745801')
	}

	stages {
		 stage('Initialize'){
        def dockerHome = tool 'myDocker'
        env.PATH = "${dockerHome}/bin:${env.PATH}"
    }

		stage('Build') {

			steps {
				sh 'docker build -t 745801/whiteboard:latest .'
			}
		}

		stage('Login') {

			steps {
				sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
			}
		}

		stage('Push') {

			steps {
				sh 'docker push 745801/whiteboard:latest'
			}
		}
	}

	post {
		always {
			sh 'docker logout'
		}
	}

}
