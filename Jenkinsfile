pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Building the code...'
                sh 'mvn clean install'
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit and integration tests...'
                sh 'mvn test'
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Running code analysis...'
                sh 'sonar-scanner'
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Performing security scan...'
                sh 'dependency-check.sh'
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to Staging...'
                sh 'aws deploy'
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on Staging...'
                sh 'run-integration-tests'
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to Production...'
                sh 'aws deploy'
            }
        }
    }
    post {
        success {
            echo 'Pipeline completed successfully.'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}
post {
    success {
        emailext body: 'Stage completed successfully', 
                 subject: 'Jenkins Pipeline Success', 
                 to: 'chenuperera13@gmail.com', 
                 attachmentsPattern: '**/*.log'
    }
    failure {
        emailext body: 'Stage failed', 
                 subject: 'Jenkins Pipeline Failed', 
                 to: 'chenuperera13@gmail.com', 
                 attachmentsPattern: '**/*.log'
    }
}

