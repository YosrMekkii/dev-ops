pipeline {
    agent any

    tools {
        maven 'M2_HOME'
    }

    stages {
        stage('GIT') {
            steps {
                git(
                    branch: 'main',
                    url: 'https://github.com/YosrMekkii/dev-ops.git'
                )
            }
        }
                stage('compile') {
            steps {
                echo "🛠️ Compilation du projet avec Maven..."
                sh 'mvn clean compile'
            }
        }
        stage('SonarQube Analysis') {
            steps {
                sh 'mvn sonar:sonar -Dsonar.token=sqa_3ebf5bb268e905d75f60f89702ee4d5ac1489f9b -Dmaven.test.skip=true'
            }
        }
    }
}

