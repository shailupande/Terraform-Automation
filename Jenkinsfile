pipeline {
    agent any

    parameters {
        choice(
            name: 'BRANCH_CHOICE',
            choices: ['main', 'develop', 'feature/example', 'Other'],
            description: 'Select a branch from the common list (use override for custom branch)'
        )
        string(
            name: 'BRANCH_OVERRIDE',
            defaultValue: '',
            description: 'If set, this branch name will override BRANCH_CHOICE'
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
                    def branchToUse = (params.BRANCH_OVERRIDE?.trim()) ? params.BRANCH_OVERRIDE.trim() : params.BRANCH_CHOICE
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
