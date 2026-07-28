pipeline {
    agent any

    environment {
        // Pulls the secret token you saved in Jenkins Credentials
        RAILWAY_TOKEN = credentials('RAILWAY_TOKEN')
    }

    stages {
        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Build & Test') {
            steps {
                echo 'Running build and test suite...'
                // Add your build/test commands here (e.g., sh 'npm test' or sh './gradlew test')
            }
        }

        stage('Deploy to Railway') {
            steps {
                script {
                    echo 'Deploying application to Railway...'
                    // Uses npx to run the Railway CLI without requiring a manual install on the Jenkins agent
                    // --ci streams logs and exits when the build completes
                    sh 'npx @railway/cli up --service "robertcoder/jenkins-tools:latest" --ci'
                }
            }
        }
    }

    post {
        success {
            echo 'Deployment to Railway succeeded!'
        }
        failure {
            echo 'Pipeline failed. Check Jenkins build logs for details.'
        }
    }
}
