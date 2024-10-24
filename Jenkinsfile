pipeline {
    agent {
        label 'workstation'
    }

    options {
        timeout(time: 30, unit: 'MINUTES')
        disableConcurrentBuilds()
        ansiColor('xterm')
    }

    parameters {
        string(name: 'appVersion', defaultValue: '1.0.0', description: 'Application version to deploy')
    }

    stages {
        stage('Print the Version') {
            steps {
                echo "Received Application version: ${params.appVersion}"
            }
        }

        stage('Init') {
            steps {
                sh """
                cd terraform
                terraform init
                """
            }
        }

        stage('Plan') {
            steps {
                sh """
                cd terraform
                terraform plan -var="app_version=${params.appVersion}"
                """
            }
        }

        // Uncomment the Deploy stage when ready
        // stage('Deploy') {
        //     steps {
        //         sh """
        //         cd terraform
        //         terraform apply -auto-approve -var="app_version=${params.appVersion}"
        //         """
        //     }
        // }
    }

    post {
        always {
            echo 'Cleaning up workspace...'
            deleteDir()
        }
        success {
            echo 'Deployment succeeded!'
        }
        failure {
            echo 'Deployment failed!'
        }
    }
}

// // it is down stream job
// pipeline {
//     agent {
//         label 'workstation'
//     }
//     options {
//         timeout(time: 30, unit: 'MINUTES')
//         disableConcurrentBuilds()
//         ansiColor('xterm')
//     }
//     parameters {
//         string(name: 'appVersion', defaultValue: '1.0.0', description: 'What is the application version?')
//     }
//     environment{
//         def appVersion = ''
//     }
//     stages {
//         stage('print the version'){
//             steps{
//                 script{
//                     echo "Application version: ${params.appVersion}"
//                 }
//             }
//         }
//         stage('Init'){
//             steps{
//                 sh """
//                     cd terraform
//                     terraform init
//                 """
//             }
//         }
//         stage('Plan'){
//             steps{
//                 sh """
//                     pwd
//                     cd terraform
//                     terraform plan -var="app_version=${params.appVersion}"
//                 """
//             }
//         }
//
// //         stage('Deploy'){
// //             steps{
// //                 sh """
// //                     pwd
// //                     cd terraform
// //                     terraform apply -auto-approve -var="app_version=${params.appVersion}"
// //                 """
// //             }
// //         }
//     }
//     post {
//         always {
//             echo 'I will always say Hello again!'
//             deleteDir()
//         }
//         success {
//             echo 'I will run when pipeline is success'
//         }
//         failure {
//             echo 'I will run when pipeline is failure'
//         }
//     }
// }