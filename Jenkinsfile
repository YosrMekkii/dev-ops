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
                sh 'mvn sonar:sonar -Dsonar.token=squ_99c7ba191bbe8a862001a96a1e4dc076c8c3e12e -Dmaven.test.skip=true'
            }
        }
    }
}

