pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/berezovsky13/python.git'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    sh '''
                      docker run --rm \
                        -v "$PWD:/usr/src" \
                        -w /usr/src \
                        -e SONAR_TOKEN="${SONAR_TOKEN}" \
                        -e SONAR_HOST_URL="${SONAR_HOST_URL}" \
                        sonarsource/sonar-scanner-cli:latest
                    '''
                }
            }
        }
    }
}
