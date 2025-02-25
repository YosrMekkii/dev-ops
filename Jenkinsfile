pipeline {
    agent any

    stages {
        stage('SonarQube Analysis') {
            steps {
                withCredentials([
                    string(credentialsId: 'SONAR_TOKEN', variable: 'SONAR_TOKEN')
                ]) {
                    sh 'mvn sonar:sonar -Dsonar.login=$SONAR_TOKEN -Dmaven.test.skip=true'
                }
            }
        }
    }
}
