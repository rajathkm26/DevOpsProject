pipeline {

  environment {
    registry = "rajathkm26/docker-jenkins-pipeline"
    registryCredential = 'rajath'
  }
  agent any
  stages {
    stage('Cloning Git') {
      steps {
          git  'https://github.com/rajathkm26/DevOpsProject.git'
	}
    }
    stage('Docker Build') {
      agent any
      steps {
	sh 'git clone https://github.com/rajathkm26/DevOpsProject.git'
        sh 'docker build -t jenkins-docker:1.0 ./DevOpsProject'
      }
    }
    stage('Deploy Image') {
      steps{
        script {
            docker.withRegistry( '', registryCredential ) {
            sh 'docker push jenkins-docker:1.0'
          }
        }
      }
    }
    stage('Remove Unused docker image') {
      steps{
        sh "docker rmi $registry:$BUILD_NUMBER"
      }
    }
  }
}
