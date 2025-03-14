pipeline {
    agent any

    environment {
        SONARQUBE_SERVER = "SonarQube"
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/Shrishti-Gupta-Tech/CI-CD-pipline-resume.git'
            }
        }

        stage('Build Backend') {
            steps {
                dir('resume-ai-backend') {
                    sh './mvnw clean package -DskipTests'
                }
            }
        }

        stage('Build Frontend') {
            steps {
                dir('resume_frontend') {
                    sh 'npm install && npm run build'
                }
            }
        }

        stage('SonarQube Analysis') {
            steps {
                dir('resume_backend') {
                    withSonarQubeEnv('SonarQube') {
                        sh './mvnw sonar:sonar'
                    }
                }
            }
        }
    }

    post {
        success {
            echo '✅ Build Successful!'
        }
        failure {
            echo '❌ Build Failed!'
        }
    }
}
