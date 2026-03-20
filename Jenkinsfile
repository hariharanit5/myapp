pipeline {
    agent any

    tools {
        jdk 'jdk21'
        gradle 'gradle'
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/hariharanit5/myapp.git'
            }
        }

        stage('Build') {
            steps {
                sh 'gradle clean build'
            }
        }

        stage('Test') {
            steps {
                sh 'gradle test'
            }
        }

        stage('Archive WAR') {
            steps {
                archiveArtifacts artifacts: 'build/libs/*.war'
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
}
