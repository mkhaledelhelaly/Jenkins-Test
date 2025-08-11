pipeline {
    agent any
    stages {
        stage('Clone Repo') {
            steps {
                git 'https://github.com/mkhaledelhelaly/Jenkins-Test.git'
            }
        }
        stage('Build') {
            steps {
                echo 'Building...'
            }
        }
        stage('Test') {
            steps {
                echo 'Running tests...'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying...'
            }
        }
    }
}
