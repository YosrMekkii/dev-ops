pipeline {
    agent any

    stages {
        stage('SonarQube Analysis') {
            steps {
                withCredentials([string(credentialsId: 'SONAR_TOKEN', variable: 'SONAR_TOKEN')]) {
                    sh 'mvn sonar:sonar -Dsonar.login=$SONAR_TOKEN -Dmaven.test.skip=true'
                }
            }
        }

        stage('Deploy to Nexus') {
            steps {
                withCredentials([
                    string(credentialsId: 'nexus-username', variable: 'NEXUS_USERNAME'),
                    string(credentialsId: 'nexus-password', variable: 'NEXUS_PASSWORD')
                ]) {
                    script {
                        try {
                            sh """
                                echo "Deploying to Nexus..."
                                mvn deploy -DrepositoryId=deploymentRepo \
                                           -Durl=http://172.17.0.1:8081/repository/maven-releases/ \
                                           -X
                            """
                        } catch (Exception e) {
                            error "Deployment failed: ${e.getMessage()}"
                        }
                    }
                }
            }
        }
    }
}
