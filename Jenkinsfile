pipeline {
    agent {
        label 'workstation'
    }

    options {
        ansiColor('xterm')
        disableConcurrentBuilds()
    }

    parameters {
        string(name: 'AppVersion', defaultValue: '1.0.0', description: 'What is the app version?')
    }

    environment {
        appVersion = "${params.AppVersion}"
        component = 'backend'
    }

    stages {
        stage('App Version') {
            steps {
                script {
                echo "App Version is: ${params.appVersion}"
                }
            }
        }
        stage('Terraform Init') {
            steps {
                script {
                    sh '''
                    pwd
                    cd terraform
                    terraform init
                    '''
                }
            }
        }

        stage('Terraform Plan') {
            steps {
                script {
                    sh '''
                    cd terraform
                    terraform plan -var="app_version=${params.appVersion}"
                    '''
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
            echo 'I will run when the pipeline is successful'
        }
        failure {
            echo 'I will run when the pipeline fails'
        }
    }
}
