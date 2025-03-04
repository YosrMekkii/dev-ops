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


        stage('Deploy to Nexus') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'nexus-credentials', usernameVariable: 'NEXUS_USERNAME', passwordVariable: 'NEXUS_PASSWORD')]) {
    sh """
        mvn deploy -DrepositoryId=deploymentRepo \
                   -Durl=http://172.17.0.1:8081/repository/maven-releases/ \
                   -Dusername=$NEXUS_USERNAME \
                   -Dpassword=$NEXUS_PASSWORD
    """
             }
         }
    }
}
