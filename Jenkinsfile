pipeline {
    agent any
    tools{ nodejs 'NodeJS 22.9.0'}
        
        environment {
        DEPLOY_HOOK_URL = 'https://api.render.com/deploy/srv-cron79pu0jms73cc4720?key=PaAZ3Dxt0jU' 
       SLACK_CHANNEL = 'C07NDBQ7LDC,#ip1-assingment'
       SLACK_COLOR = 'good'
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

        stage('Install my Dependencies') {
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



            stage('Deploy to Onrender.com') {
                        steps {
                            script {
                                def response = sh(script: """
                                    curl -X POST ${DEPLOY_HOOK_URL}
                                """, returnStdout: true).trim()
                                
                                echo "Deployment Response: ${response}"
                            }
                        }

                    }

       stage('Notify Slack') {
            steps {
                // Send Slack notification on successful deploy
                slackSend channel:'josephip1', color: 'good', message: "Build #${env.BUILD_NUMBER} deployed successfully. View at: ${env.RENDER_URL}"
            } 
            

    }
    }


    post {
        success {
            echo 'Pipeline succeeded!'
            slackSend(channel: env.SLACK_CHANNEL, message: "Job '${env.JOB_NAME}' (#${env.BUILD_NUMBER}) succeeded!", color: env.SLACK_COLOR)
        }
        failure {
            echo 'Pipeline failed!'
            slackSend(channel: env.SLACK_CHANNEL, message: "Job '${env.JOB_NAME}' (#${env.BUILD_NUMBER}) failed!", color: 'danger')
        }
    }
}
