pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/SamVESIT/devops-practical.git' // Replace with your repo
            }
        }

        stage('Build') {
            steps {
                dir('my-app') {  // Ensure this matches your project structure
                    echo 'Building the project...'
                    bat 'mvn clean package'  // Use 'sh' instead of 'bat' for Linux
                }
            }
        }

        stage('Archive Artifacts') {
            steps {
                archiveArtifacts artifacts: '**/target/*.war', onlyIfSuccessful: true
            }
        }
    }

    post {
        success {
            echo 'Build succeeded'
        }
        failure {
            script {
                echo 'Build failed'
                currentBuild.result = 'FAILURE'
            }
        }
        always {
            echo 'Pipeline execution completed!'
        }
    }
}
