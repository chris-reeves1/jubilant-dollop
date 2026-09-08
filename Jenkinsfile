pipeline {
    agent any

    environment {
        SONAR_HOST_URL    = "http://172.31.23.181:9000"
        SONAR_PUBLIC_URL  = "http://3.8.177.73:9000"
        SONAR_PROJECT_KEY = "flask-app"
    }

    stages {

        stage('SonarQube Scan') {
            steps {
                withCredentials([
                    string(
                        credentialsId: 'sonarqube-token',
                        variable: 'SONAR_TOKEN'
                    )
                ]) {
                    sh '''
                        docker run --rm \
                            -e SONAR_HOST_URL="$SONAR_HOST_URL" \
                            -e SONAR_TOKEN="$SONAR_TOKEN" \
                            -v "$WORKSPACE:/usr/src" \
                            sonarsource/sonar-scanner-cli \
                            -Dsonar.projectKey="$SONAR_PROJECT_KEY" \
                            -Dsonar.sources=. \
                            -Dsonar.exclusions=".venv/**,venv/**,__pycache__/**,**/*.pyc"
                    '''
                }
            }
        }

        stage('Manual Quality Gate Check') {
            steps {
                input(
                    message: "Check the Quality Gate in SonarQube: ${SONAR_PUBLIC_URL}",
                    ok: "Proceed"
                )
            }
        }
    }
}
