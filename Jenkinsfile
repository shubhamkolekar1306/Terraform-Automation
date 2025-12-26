pipeline {
    agent any

    parameters {
        choice(
            name: 'ACTION',
            choices: ['plan', 'apply', 'destroy'], // Added destroy
            description: 'Select the action to perform'
        )
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scmGit(
                    branches: [[name: '*/main']],
                    extensions: [],
                    userRemoteConfigs: [[url: 'https://github.com/shubhamkolekar1306/Terraform-Automation.git']]
                )
            }
        }

        stage("Terraform Init") {
            steps {
                sh "terraform init -reconfigure"
            }
        }

        stage("Action") {
            steps {
                script {
                    switch (params.ACTION) {
                        case 'plan':
                            echo 'Executing Plan...'
                            sh "terraform plan"
                            break
                        case 'apply':
                            echo 'Executing Apply...'
                            sh "terraform apply --auto-approve"
                            break
                        case 'destroy':
                            echo 'Executing Destroy...'
                            sh "terraform destroy --auto-approve"
                            break
                        default:
                            error 'Unknown action selected!'
                    }
                }
            }
        }
    }
}
