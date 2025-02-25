pipeline {
    agent any

    tools {
        maven 'M2_HOME'
    }

    stages {
        stage('GIT') {
            steps {
                git(
                    branch: 'master',
                    url: 'https://github.com/khalil27/dev-ops.git'
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
                sh 'mvn sonar:sonar -Dsonar.token=squ_2760a0ff4007b684d219ac215337e442d4e0e809 -Dmaven.test.skip=true'
            }
        }
    }
}

