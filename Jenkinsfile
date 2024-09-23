pipeline {
    agent any
    tools{ nodejs 'NodeJS 22.9.0'}
        
        environment {
        DEPLOY_HOOK_URL = 'https://api.render.com/deploy/srv-cron79pu0jms73cc4720?key=PaAZ3Dxt0jU' 
      
    }

    triggers {
        
        githubPush()
        
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



            stage('Deploy to Render122') {
                        steps {
                            script {
                                def response = sh(script: """
                                    curl -X POST ${DEPLOY_HOOK_URL}
                                """, returnStdout: true).trim()
                                
                                echo "Deployment Response: ${response}"
                            }
                        }

                    }
                // Deployment commands (e.g., copying files, running scripts)
               
                // Add your deployment commands here
            

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
