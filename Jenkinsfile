pipeline {
    agent {
        label 'AGENT-1'
    }
    options {
        // Timeout counter starts BEFORE the agent is allocated
        timeout(time: 30, unit: 'MINUTES')
        disableConcurrentBuilds()
        // retry(1)
    }
    environment { 
        DEBUG = 'true'
        appVersion = ''  // Can also be initialized here if you prefer
    }
    stages {
        stage('Read the version') {
            steps {
                script { 
                    def packageJson = readJSON file: 'package.json'

                    appVersion = packageJson.version
                    echo "App version: ${appVersion}"
                }
            }
        }
        stage('Install Dependencies')
            steps { 
                sh "npm install"
            }
        }
        stage('Docker build')
            {
            steps {
                sh """
                docker build -t prameela0/backend:${appVersion} .
                docker images
                """
                
            }
        }
    }
    post {
        always {
            echo "this section runs always"
            deleteDir()
        }
        success {
            echo "this section runs when pipeline is successful"
        }
        failure {
            echo "this section runs when pipeline fails"
        }
    }
}
