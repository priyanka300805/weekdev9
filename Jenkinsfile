pipeline {
    agent any
   
    stages {

        stage('Build Docker Image') {
            steps {
                echo "Build Docker Image"
                bat "docker build -t seleniumdemoapp:v1 ."
            }
        }
        stage('Docker Login') {
            steps {
                  bat 'docker login -u erumfaiz -p Erum@3005'
                }
            }
        stage('push Docker Image to Docker Hub') {
            steps {
                echo "push Docker Image to Docker Hub"
                bat "docker tag seleniumdemoapp:v1 erumfaiz/sample:seleniumtestimage"               
                    
                bat "docker push erumfaiz/sample:seleniumtestimage"
                
            }
        }
        stage('Deploy to Kubernetes') { 
            steps { 
                    // apply deployment & service 
                    bat 'kubectl apply -f deployment.yaml --validate=false' 
                    bat 'kubectl apply -f service.yaml' 
            } 
        }
    }
    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Please check the logs.'
        }
    }
}
