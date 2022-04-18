pipeline {

  agent docker
  environment {
		DOCKERHUB_CREDENTIALS=credentials('dockerhub-cred-usman')
	}


  stages {
    
    

    stage('Checkout Source') {
      steps {
        git url:'https://github.com/Muhammad-Imtiaz/k8s-jenkins.git', branch:'master'
      }
    }
    
    stage('Build') {

			steps {
				sh 'docker build -t bharathirajatut/nodeapp:latest .'
			}
		}

		stage('Login') {

			steps {
				sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
			}
		}

		stage('Push') {

			steps {
				sh 'docker push bharathirajatut/nodeapp:latest'
			}
		}
    


    stage('Deploy App') {
      steps {
        script {
          kubernetesDeploy(configs: "deployment.yaml", kubeconfigId: "mykubeconfig1")
        }
      }
    }

  }
}
