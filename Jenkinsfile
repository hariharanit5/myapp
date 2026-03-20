pipeline {
    agent any

    tools {
        jdk 'jdk21'
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/hariharanit5/myapp.git'
            }
        }

        stage('Build') {
            steps {
                sh 'chmod +x gradlew'
                sh './gradlew clean build'
            }
        }

        stage('Test') {
            steps {
                sh './gradlew test'
            }
        }

        stage('Archive WAR') {
            steps {
                archiveArtifacts artifacts: 'build/libs/*.war', fingerprint: true
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                sh '''
                cp build/libs/*.war /home/ubuntu/tomcat/webapps/
                '''
            }
        }
    }

    post {
        success {
            echo '✅ Build & Deployment Successful'
        }
        failure {
            echo '❌ Pipeline Failed'
        }
    }
}
