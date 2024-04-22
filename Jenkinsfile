pipeline {
    agent any 

    stages { 
        stage('SCM Checkout') {
            steps {
                retry(3) {
                    git branch: 'main', url: 'https://github.com/satha-1/4321-Soysa'
                }
            }
        }
        stage('Build Docker Image') {
            steps {  
                bat 'docker build -t sathsara/nodeapp-cuban:%BUILD_NUMBER% .'
            }
        }
        stage('Login to Docker Hub') {
            steps {
                
                withCredentials([string(credentialsId: 'test-dockerhubpassword', variable: 'test-dockerhubpass')]) {
   
               bat'docker login -u sathsara -p ${test-dockerhubpass}'
                }
            }
        }
        stage('Push Image') {
            steps {
                bat 'docker push sathsara/nodeapp-cuban:%BUILD_NUMBER%'
            }
        }
    }
    post {
        always {
            bat 'docker logout'
        }
    }
}