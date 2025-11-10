pipeline {
    agent any 

    tools {
        maven 'Maven3'
        jdk 'JDK17'
    }

    triggers {
        githubPush()
    }

    stages {

        stage('Checkout') {
            steps {
                git(
                branch: 'main',
                credentialsId: 'git-cred',
                url: 'https://github.com/himanshurkt96/Java-app.git'
            )}
        }

        stage('Build') {
            steps {
                sh 'mvn clean install -DskipTests'
            }
        }

        stage('Run Unit Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Deploy Locally') {
            steps {
                sh """
                echo "Stopping existing application..."
                pkill -f 'java -jar' || true

                echo "Starting application..."
                nohup java -jar target/*.jar > app.log 2>&1 &
                """
            }
        }
    }
}
