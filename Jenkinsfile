pipeline {
    agent { label 'windows' } // Ensure your Windows agent has the 'windows' label

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', credentialsId: 'your-git-credentials', url: 'https://github.com/your-username/my-jenkins-app.git'
            }
        }
        stage('Build') {
            steps {
                bat 'echo "Building the application..."'
                bat 'mkdir target'
                bat 'echo "Application built successfully!" > target\\output.txt'
            }
        }
        stage('Test') {
            steps {
                bat 'echo "Running tests..."'
                bat 'if exist target\\output.txt (echo "Tests passed!") else (exit 1)'
            }
        }
        stage('Deploy to Staging') {
            steps {
                bat 'echo "Deploying to Staging environment..."'
                bat 'mkdir C:\\staging'
                bat 'copy target\\output.txt C:\\staging\\'
                bat 'echo "Deployed to Staging!"'
            }
        }
        stage('Deploy to Production') {
            when {
                branch 'main'
            }
            steps {
                bat 'echo "Deploying to Production environment..."'
                bat 'mkdir C:\\production'
                bat 'copy target\\output.txt C:\\production\\'
                bat 'echo "Deployed to Production!"'
            }
        }
    }
    post {
        always {
            echo 'Pipeline finished!'
        }
        success {
            echo 'Build successful!'
        }
        failure {
            echo 'Build failed!'
        }
    }
}
