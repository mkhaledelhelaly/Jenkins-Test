pipeline {
    agent any

    parameters {
        string(name: 'BRANCH_NAME', defaultValue: 'main', description: 'Git branch to build from')
        choice(name: 'DEPLOY_ENV', choices: ['dev', 'staging', 'prod'], description: 'Deployment environment')
    }

    environment {
        REPO_URL = 'https://github.com/mkhaledelhelaly/Jenkins-Test.git'
    }

    stages {
        stage('Clone Repo') {
            steps {
                git branch: "${params.BRANCH_NAME}", url: "${env.REPO_URL}"
            }
        }

        stage('Build') {
            steps {
                echo "Building application from branch: ${params.BRANCH_NAME}"
                sh 'mkdir -p build && echo "Build output" > build/output.txt'
            }
        }

        stage('Tests') {
            parallel {
                stage('Unit Tests') {
                    steps {
                        echo 'Running unit tests...'
                        sh 'sleep 2'
                    }
                }
                stage('Integration Tests') {
                    steps {
                        echo 'Running integration tests...'
                        sh 'sleep 3'
                    }
                }
            }
        }

        stage('Archive Artifacts') {
            steps {
                archiveArtifacts artifacts: 'build/**', fingerprint: true
            }
        }

        stage('Deploy') {
            steps {
                echo "Deploying to ${params.DEPLOY_ENV} environment..."
            }
        }
    }

    post {
        success {
            echo '✅ Pipeline completed successfully!'
        }
        failure {
            echo '❌ Pipeline failed!'
        }
        always {
            echo '📦 Cleaning up workspace...'
            cleanWs()
        }
    }
}
