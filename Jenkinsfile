pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Le code est recupere depuis Git.'
            }
        }

        stage('Build') {
            steps {
                echo 'Preparation de l application.'
                sh 'test -f application/index.html'
                sh 'test -f application/Dockerfile'
            }
        }

        stage('Test') {
            steps {
                echo 'Verification du contenu.'
                sh "grep -q 'Projet CI/CD' application/index.html"
            }
        }

        stage('Security') {
            steps {
                echo 'Etape reservee a SonarQube et OWASP ZAP.'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Etape de deploiement a configurer ensuite.'
            }
        }
    }

    post {
        success {
            echo 'Pipeline termine avec succes.'
        }
        failure {
            echo 'Echec du pipeline.'
        }
    }
}
