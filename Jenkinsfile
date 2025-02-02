pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Get code from GitHub repository
                git branch: 'main', 
                    url: 'https://github.com/Gaurav12341234/CI-CD-React-App.git'
            }
        }

        stage('Install') {
            steps {
                // Install Node dependencies
                sh 'npm install'
            }
        }

        stage('Lint') {
            steps {
                script {
                    try {
                        sh 'npm run lint'
                    } catch (err) {
                        // Don't fail the build, but mark it as unstable
                        unstable(message: "Linting issues found")
                        // Continue with the build
                        echo "Lint issues found, but continuing with build..."
                    }
                }
            }
        }

        stage('Build') {
            steps {
                // Create production build
                sh 'npm run build'
            }
        }

        stage('Deploy') {
            steps {
                echo "Deploy success"
            }
        }
    }

    post {
        success {
            echo 'Build and deployment successful!'
        }
        unstable {
            echo 'Build completed with some issues.'
        }
        failure {
            echo 'Build or deployment failed!'
        }
    }
}
