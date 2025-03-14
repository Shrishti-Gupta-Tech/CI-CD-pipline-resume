pipeline {
    agent any

    environment {
        SONARQUBE_SERVER = "SonarQube"
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/Shrishti-Gupta-Tech/ai_based_resume_generator.git'
            }
        }

        stage('Build Backend') {
            steps {
                dir('ai_based_resume_generator/resume_backend') {
                    sh './mvnw clean package -DskipTests'
                }
            }
        }

        stage('Build Frontend') {
            steps {
                dir('ai_based_resume_generator/resume_frontend') {
                    sh 'npm install && npm run build'
                }
            }
        }

        stage('Run Tests') {
            steps {
                dir('ai_based_resume_generator/resume_backend') {
                    sh './mvnw test'
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
