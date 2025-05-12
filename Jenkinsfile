pipeline {
    agent any

    environment {
        SONAR_HOST_URL = 'http://sonarqube:9000'    // Using the actual container name
        SONAR_PROJECT_KEY = 'demo'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/berezovsky13/python.git'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withCredentials([string(credentialsId: 'sonar', variable: 'SONAR_TOKEN')]) {
                    sh '''
                        docker run --rm \
                          -e SONAR_TOKEN=$SONAR_TOKEN \
                          -e SONAR_HOST_URL=$SONAR_HOST_URL \
                          -v "$PWD:/usr/src" \
                          -w /usr/src \
                          sonarsource/sonar-scanner-cli:latest \
                          -Dsonar.projectKey=$SONAR_PROJECT_KEY \
                          -Dsonar.sources=. \
                          -Dsonar.host.url=$SONAR_HOST_URL \
                          -Dsonar.login=$SONAR_TOKEN
                    '''
                }
            }
        }
    }
}
