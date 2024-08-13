pipeline {
    agent any
    stages {
        // Stage 1: Initialize
        stage('Build with Maven') {
            steps {
                echo 'Builduing with Maven...'
            }
        }
        // Stage 2: Build
        stage('Build') {
            steps {
                echo 'Building the project...'
                sh 'mvn install'
            }
        }
        // Stage 3: Deploy
        stage('Deploy') {
            when {
                branch 'main' // Only deploy if we're on the main branch
            }
            steps {
                // Example deployment step, e.g., upload to a server
                sh 'scp target/your-app.jar user@yourserver:/path/to/deploy/'
            }
        }
    }
    post {
        always {
            echo 'Pipeline completed!'
        }
    }
}
