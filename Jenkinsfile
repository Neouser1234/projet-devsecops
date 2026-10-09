pipeline {
    agent { label 'semgrep' }

    stages {
        stage('Checkout') {
            steps {
                echo 'Le code est recupere depuis GitHub.'
            }
        }

        stage('Build') {
            steps {
                echo 'Verification des fichiers de l application.'
                sh 'test -f application/index.html'
                sh 'test -f application/Dockerfile'
            }
        }

        stage('Test') {
            steps {
                echo 'Verification du contenu HTML.'
                sh "grep -q 'Projet CI/CD' application/index.html"
            }
        }
        
        stage('Analyse statique - Semgrep') {
            agent { label 'semgrep' }
            steps {
                checkout scm
                echo 'Analyse statique de securite avec Semgrep.'
                sh '/opt/semgrep-venv/bin/semgrep scan --config auto --error application'
            }
        }
        
        stage('Analyse de code - SonarQube') {
            steps {
                echo 'Point d integration reserve au membre 2.'
                echo 'SonarQube sera configure avec le membre responsable.'
            }
        }

        stage('Tests de securite web - OWASP ZAP') {
            steps {
                echo 'Point d integration reserve au membre 3.'
                echo 'OWASP ZAP sera configure lorsque l application sera accessible.'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Point d integration reserve au membre 4.'
                echo 'Le deploiement sera configure avec le responsable.'
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
