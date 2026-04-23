pipeline {
    agent any

    tools {
        maven 'Maven'
    }

    stages {

        stage('Git Checkout') {
            steps {
                git branch: 'main', url: 'YOUR_GITHUB_REPO_URL'
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
                -Dsonar.login=YOUR_SONAR_TOKEN
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