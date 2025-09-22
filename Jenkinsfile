pipeline {
    agent any

    tools {
        // Make sure you configured JDK and Maven in Jenkins Global Tools
        jdk 'JDK17'      // Replace with your configured JDK name
        maven 'Maven3'   // Replace with your configured Maven name
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/manohar-b29/java-scientific-calculator.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean compile'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'   // publish test reports
                }
            }
        }

        stage('Package') {
            steps {
                sh 'mvn package -DskipTests'
            }
            post {
                success {
                    archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
                }
            }
        }

        stage('Deploy (Optional)') {
            when {
                branch 'main'
            }
            steps {
                echo 'Deploying application...'
                // Example: copy JAR to server or build Docker image
                // sh 'docker build -t my-scientific-calculator .'
            }
        }
    }

    post {
        success {
            echo '✅ Pipeline finished successfully!'
        }
        failure {
            echo '❌ Pipeline failed. Check logs!'
        }
    }
}

