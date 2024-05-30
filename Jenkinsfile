pipeline {
    agent any

    parameters {
        string(name: 'GIT_CREDENTIALS', defaultValue: 'your-credentials-id', description: 'Enter your Git Credentials ID')
        string(name: 'GIT_URL', defaultValue: 'https://github.com/koddyb/myapp.git', description: 'Enter the Git Repository URL')
        string(name: 'GIT_BRANCH', defaultValue: 'your-branch-name', description: 'Enter the Git Branch')
        string(name: 'DOCKERHUB_USERNAME', defaultValue: 'your-dockerhub-username', description: 'Enter your Docker Hub Username')
        string(name: 'APP_VERSION', defaultValue: 'latest', description: 'Enter the Application Version')
        string(name: 'APP_NAME', defaultValue: 'your-app-name', description: 'Enter your Application Name')
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
        stage('SonarQube Analysis') {
            environment {
                SONAR_SCANNER_HOME = tool 'sonar'
            }
            steps {
                withSonarQubeEnv('sonar') {
                    script {
                        sh "${SONAR_SCANNER_HOME}/bin/sonar-scanner"
                    }
                }
            }
        }
        stage('Building Application') {
            steps {
                script {
                    sh "docker build -t ${params.DOCKERHUB_USERNAME}/${params.APP_NAME}:${params.APP_VERSION}."
                }
            }
        }
    }
}
