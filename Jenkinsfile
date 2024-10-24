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
        stage('Terraform Init') {
            steps {
                script {
                    sh '''
                    pwd
                    terraform init
                    '''
                }
            }
        }

//         stage('Terraform Plan') {
//             steps {
//                 script {
//                     sh '''
//                     terraform plan -var="app_version=${appVersion}"
//                     '''
//                 }
//             }
//         }
//     }

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
