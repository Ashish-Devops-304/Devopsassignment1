pipeline {
    agent { label 'slave-node' } // Ensure your Windows agent has the 'slave-node' label

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', credentialsId: '304ashishyadav@gmail.com', url: 'https://github.com/Ashish-Devops-304/Devopsassignment1.git'
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
