
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
                sh 'docker build -t berezovsky8/python-demo:1.0.3 .'
            }
        }
        
        stage("Trivy Scan"){
            steps{
                sh 'trivy image berezovsky8/python-demo:1.0.3'
            }
        }

        stage("Docker Push"){
            steps{
                withCredentials([usernamePassword(credentialsId: 'dockerhub', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]){
                    sh '''
                        echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin
                        docker push berezovsky8/python-demo:1.0.3
                    '''
                    
                }
            }
        }
        
        stage("Docker Run"){
            steps{
                sh 'docker run python-demo:1.0.1'
            }
        }
    }
}