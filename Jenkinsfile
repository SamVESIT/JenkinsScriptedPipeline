pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/SamVESIT/JenkinsScriptedPipeline.git'
            }
        }

        stage('Build') {
            steps {
                echo 'Building the project...'
                bat 'C:\\BuildTools\\apache-maven-3.9.9\\bin\\mvn.cmd clean package'
            }
        }

        stage('List Build Output') {
            steps {
                bat 'dir /s /b target'
            }
        }

        stage('Archive Artifacts') {
            steps {
                archiveArtifacts artifacts: '**/target/*.jar', onlyIfSuccessful: true
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
