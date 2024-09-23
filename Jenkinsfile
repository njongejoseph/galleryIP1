pipeline {
    agent any
    triggers {
        
        githubPush()
        
    }

    environment {
        NODE_HOME = tool name: 'NodeJS', type: 'NodeJSInstallation'
        PATH = "${NODE_HOME}/bin:${env.PATH}"
    }

    stages {
        stage('Checkout') {
            steps {
                // Clone the repository
                git credentialsId: 'ef700935-287d-4406-84b9-65f2ed792bc6', url: 'https://github.com/njongejoseph/galleryIP1'
            }
        }

        stage('Install Dependencies') {
            steps {
                // Install Node.js dependencies
                sh 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                // Run your test suite
                // sh 'npm test'
                echo 'Testing the application...'
            }
        }

        stage('Build') {
            steps {
                // Build your application (if needed)
                //sh 'npm run build'
                echo 'Building the application...'
            }
        }

        stage('Deploy') {
            steps {
                // Deployment commands (e.g., copying files, running scripts)
                echo 'Deploying the application...'
                // Add your deployment commands here
            }
        }
    }

    post {
        success {
            echo 'Pipeline succeeded!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
