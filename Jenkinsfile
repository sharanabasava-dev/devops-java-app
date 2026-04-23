pipeline {
    agent any

    tools {
        maven 'Maven'
    }

    stages {

        stage('Git Checkout') {
            steps {
                git branch: 'main', url: https://github.com/sharanabasava-dev/devops-java-app.git
            }
        }

        stage('Build') {
            steps {
                bat 'mvn clean package'
            }
        }

        stage('SonarQube Scan') {
            steps {
                bat '''
                mvn sonar:sonar ^
                -Dsonar.projectKey=devops-java-app ^
                -Dsonar.host.url=http://localhost:9000 ^
                -Dsonar.login=sqp_a9953dca665f70bc21b84421d61ccee04b5b9f6f
                '''
            }
        }

        stage('Docker Build') {
            steps {
                bat 'docker build -t javaapp:v1 .'
            }
        }

        stage('Deploy') {
            steps {
                bat 'kubectl apply -f deployment.yaml'
            }
        }
    }
}