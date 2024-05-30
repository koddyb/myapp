pipeline {
    agent any
    
    parameters {
        string(name: 'GIT_CREDENTIALS', defaultValue: 'your-credentials-id', description: 'Enter your Git Credentials ID')
        string(name: 'GIT_URL', defaultValue: 'https://github.com/koddyb/myapp.git', description: 'Enter the Git Repository URL')
        string(name: 'GIT_BRANCH', defaultValue: 'your-branch-name', description: 'Enter the Git Branch')
    }

    stages {
        stage('Clean Workspace') {
            steps {
                cleanWs()
            }
        }
        stage('Cloning the Repository') {
            steps {
                git branch: "${params.GIT_BRANCH}", 
                    credentialsId: "${params.GIT_CREDENTIALS}", 
                    url: "${params.GIT_URL}"
            }
        }
    }
}
