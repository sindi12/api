pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                echo 'Checkout-ing project'
                git 'https://github.com/sindi12/api.git'
                echo 'Checkout Success!'
            }
        }
        stage('Build Artifact') {
            steps {
                echo 'Building artifact...'
                sh 'mvn clean install'
                echo 'Success'
            }
        }
        stage('Create artifact copy') {
            steps {
                sh 'cp target/apigateway-*.jar target/apigateway.jar'
            }
        }
        
        stage('Create Docker Image') {
            steps {
                sh 'docker build -t api_gateway_image .'
            }
        }
        stage('Run Container') {
            steps {              
                sh 'docker run -d -p 8090:8080 --name demoServer api_gateway_image'           
            }
        }
    }
}
