pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building Java project...'
                bat 'javac Hello.java'
            }
        }

        stage('Test') {
            steps {
                echo 'Testing Java project...'
                bat 'java Hello'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deployment completed successfully!'
            }
        }
    }
}