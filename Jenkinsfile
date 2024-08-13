pipeline {
    agent any
 
    environment {
        JAVA_HOME = tool name: 'JDK11', type: 'jdk' // Assuming JDK11 is installed
        PATH = "${env.JAVA_HOME}/bin:${env.PATH}"
    }
 
    stages {
        stage('Checkout') {
            steps {
                // Clone the repository
                git 'https://your-repo-url.git'
            }
        }
 
        stage('Build') {
            steps {
                // Build the project using Maven
                sh 'mvn clean compile'
            }
        }
 
        stage('Test') {
            steps {
                // Run the tests
                sh 'mvn test'
            }
            post {
                always {
                    // Archive test results and logs
                    junit '**/target/surefire-reports/*.xml'
                }
            }
        }
 
        stage('Package') {
            steps {
                // Package the application
                sh 'mvn package'
            }
            post {
                success {
                    archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true
                }
            }
        }
 
        stage('Deploy') {
            when {
                branch 'master' // Only deploy if we're on the main branch
            }
            steps {
                // Example deployment step, e.g., upload to a server
                sh 'scp target/your-app.jar ec2-user@13.202.177.58:/home/ec2-user/artifact'
            }
        }
    }
 
    post {
        always {
            // Clean up workspace
            cleanWs()
        }
    }
}
