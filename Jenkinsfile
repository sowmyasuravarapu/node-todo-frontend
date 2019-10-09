node {
    
	

    env.AWS_ECR_LOGIN=true
    def newApp
    def registry = '11vv/nodeanddocker'
    def registryCredential = 'dockerhub'
	
	stage('Git') {
		git 'https://github.com/sowmyasuravarapu/node-todo-frontend'
	}
	stage('Build') {
		sh 'npm install'
	}
	stage('Test') {
		sh 'npm test'
	}
	 stage('Building image') {
      
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
      
    }
	 stage('Deploy Image') {
      
         script {
            docker.withRegistry( '', registryCredential ) {
            dockerImage.push()
          }
        }
      
    }
    stage('Removing image') {
        sh "docker rmi $registry:$BUILD_NUMBER"
        sh "docker rmi $registry:latest"
    }
    
}
