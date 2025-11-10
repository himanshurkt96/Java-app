pipeline {
    agent any 
    tools {
        maven 'Maven3'
        jdk 'JDK17'
    }

    stages {
        stage('Checkout'){
            steps{
                git branch: 'main'
                url:
            }
        }
    

    
        stage('Build') {
        steps{
            sh 'mvn clean install -DskipTests'
        }
        }
    stage('Run Unit Test') {
        steps {
            sh 'mvn run test'
        }
    }

    stage('Deploy Locally') {

        steps {
            steps """
            echo "Stopping existing application"
            pkill -f 'java -jar' || true

            echo 'Starting Application'
            nohup java -jar target/*.jar > app.log 


            """
        }
    }
    }
}
