pipeline{
    agent any
    stages{
        stage("Checkout Code"){
            steps{
                git branch: 'main', url:'https://github.com/berezovsky13/python-DevOps-Course.git'
            }
        }
        
        stage("Docker Build+Tag"){
            steps{
                sh 'docker build -t python-demo:1.0.1 .'
            }
        }
        
        stage("Docker Run"){
            steps{
                sh 'docker run python-demo:1.0.0'
            }
        }
    }
}