
pipeline {
    agent any

    tools {
        maven 'Maven-Homebrew'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
                echo 'GitHub checkout completed'
            }
        }

        stage('Build and Test') {
            steps {
                sh 'mvn clean verify'
            }
        }

        stage('Snyk Dependency Scan') {
            steps {
                snykSecurity(
                    snykInstallation: 'Snyk-CLI',
                    snykTokenId: 'snyk-api-token',
                    severity: 'high',
                    failOnIssues: true
                )
            }
        }
    }

    post {
        success {
            echo 'Build and security scan passed!'
        }

        failure {
            echo 'Pipeline failed: check build or security findings'
        }

        always {
            echo 'CI/CD pipeline execution finished'
        }
    }
}
