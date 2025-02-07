pipeline {
    agent any 

    environment {
        MAVEN_HOME = tool 'Maven' // Use Maven installed in Jenkins
        PATH = "${MAVEN_HOME}/bin;${env.PATH}" // Add Maven to PATH
    }

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/YOUR_USERNAME/java-jenkins-demo.git'
            }
        }

        stage('Build with Maven') {
            steps {
                bat 'mvn clean package'
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
                         to: 'saravind@sirahu.com'
            }
        }
    }

    post {
        always {
            echo 'Cleaning up workspace...'
            bat 'rd /s /q *' // Windows equivalent of deleteDir()
        }
    }
}
