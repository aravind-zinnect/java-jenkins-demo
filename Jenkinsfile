pipeline {
    agent any 

    environment {
        MAVEN_HOME = tool 'maven123' // Use the name from Jenkins settings
        PATH = "${MAVEN_HOME}/bin;${env.PATH}" // Add Maven to PATH
    }

    stages {
        stage('Clone Repository') {
            steps {
        git branch: 'main', url: 'https://github.com/aravind-zinnect/java-jenkins-demo.git'
    }
        }

        stage('Build with Maven') {
            steps {
                bat '"%MAVEN_HOME%\\bin\\mvn" clean package'
            }
        }

        stage('Archive Artifacts') {
            steps {
                archiveArtifacts artifacts: 'target\\*.jar', fingerprint: true
            }
        }

        stage('Post-Build Notification') {
            steps {
                emailext subject: "Jenkins Build - ${currentBuild.fullDisplayName}",
                         body: "Build ${currentBuild.result}: Check Jenkins for details.",
                         to: 'your-email@example.com'
            }
        }
    }

    post {
        always {
            echo 'Cleaning up workspace...'
            cleanWs() // Jenkins built-in cleanup method
        }
    }
}
