pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
                echo "Checked out branch: \${env.BRANCH_NAME}", url: 'your-repo-url'
            }
        }

        stage('Create Scratch Org') {
            steps {
                sh 'sfdx force:org:create -f config/project-scratch-def.json -a YourScratchOrgAlias -s'
            }
        }

        stage('Push Source') {
            steps {
                sh 'sfdx force:source:push -u YourScratchOrgAlias'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'sfdx force:apex:test:run -u YourScratchOrgAlias -c -r human'
            }
        }

        stage('Delete Scratch Org') {
            steps {
                sh 'sfdx force:org:delete -u YourScratchOrgAlias -p'
            }
        }
    }
}
