pipeline {
    agent any

    tools {
        maven 'Maven'
    }

    stages {

        stage('Git Checkout') {
    steps {
        git branch: 'main', url: 'https://github.com/sharanabasava-dev/devops-java-app.git'
    }
}

        stage('Build') {
    steps {
        dir('javaapp') {
            sh 'mvn clean package'
        }
    }
}

        stage('SonarQube Scan') {
    steps {
        dir('javaapp') {
            sh '''
            mvn sonar:sonar \
            -Dsonar.projectKey=devops-java-app \
            -Dsonar.host.url=http://host.docker.internal:9000 \
            -Dsonar.login=Ysqp_a9953dca665f70bc21b84421d61ccee04b5b9f6f
            '''
        }
    }
}

        stage('Docker Build') {
    steps {
        dir('javaapp') {
            sh 'docker build -t javaapp:v1 .'
        }
    }
}

        stage('Deploy') {
            steps {
                sh 'kubectl apply -f deployment.yaml'
            }
        }
    }
}