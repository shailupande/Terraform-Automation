pipeline {
    agent any

    parameters {
        choice(
            name: 'BRANCH',
            choices: ['main', 'develop', 'feature/example', 'shailesh'],
            description: 'Select the branch to build'
        )
        choice(
            name: 'ACTION',
            choices: ['plan', 'apply'],
            description: 'Select the action to perform'
        )
    }
    stages {
        stage('Checkout') {
            steps {
                script {
                    def branchToUse = params.BRANCH
                    echo "Checking out branch: ${branchToUse}"
                    git branch: branchToUse, url: 'https://github.com/shailupande/Terraform-Automation.git'
                }
            }
        }
    
        stage ("terraform init") {
            steps {
                sh ("terraform init -reconfigure") 
            }
        }

        stage ("Action") {
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
                        default:
                            error 'Unknown action'
                    }
                }
            }
        }
    }
}
