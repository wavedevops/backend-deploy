pipeline {
    agent {
        label 'workstation' // Use the appropriate label for your node
    }
    
    options {
        ansiColor('xterm')        // Enable ANSI color output
        disableConcurrentBuilds() // Ensure the pipeline runs only once at a time
    }
    parameters {
        string(name: 'AppVersion', defaultValue: '1.0.0', description: 'what is the app version?')
    }
    
    environment {
        // Placeholder - environment variables cannot use 'read JSON' directly.
        appVersion = '' 
        nexusUrl = 'nexus.chaitu.net/repository/backend/' // Fixed URL
        component = 'backend'
    }
    
    stages {
        stage('Print The  Version') {
            steps {
                script  {
                echo "latest app version: ${params.AppVersion}"
                }
            }
        }
    }

    post { 
        always { 
            echo 'I will always say Hello again!'
            deleteDir() // Clean up the workspace
        }
        success { 
            echo 'I will run when pipeline is successful'
        } 
        failure { 
            echo 'I will run when the pipeline fails'
        }
    }
}
