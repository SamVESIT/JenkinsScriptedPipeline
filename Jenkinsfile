pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/SamVESIT/devops-practical.git'
            }
        }

        stage('Build') {
            steps {
                dir('my-app') {  
                    echo 'Building the project...'
                    bat 'mvn clean package' 
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
