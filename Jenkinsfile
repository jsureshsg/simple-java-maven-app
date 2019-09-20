pipeline {
   
   agent {
    docker {
        image 'maven:3-alpine'
        label 'docker'
        registryUrl 'https://hub.docker.com/'
        registryCredentialsId 'dockerhub'
    }
}
	
    stages {
        
		stage('git checkout')
		{
		   steps{
		   checkout scm
		   }
		}
		
		stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Deliver') {
            steps {
                sh './jenkins/scripts/deliver.sh'
            }
        }
    }
}
