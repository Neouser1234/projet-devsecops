pipeline {
    agent { label 'semgrep' }

    environment {
        IMAGE     = 'projet-devsecops-app'
        CONTAINER = 'app-test'
        NET       = 'test-net'
        HOST_PORT = '8081'
    }
    triggers { pollSCM('H/2 * * * *') }

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
                sh 'docker build -t ${IMAGE}:${BUILD_NUMBER} -t ${IMAGE}:latest application/'
                sh 'docker images | grep ${IMAGE}'
            }
        }

        stage('Test') {
            steps {
                echo 'Verification du contenu HTML.'
                sh "grep -q 'Projet CI/CD' application/index.html"
            }
        }

        stage('Analyse statique - Semgrep') {
            steps {
                echo 'Analyse statique de securite avec Semgrep.'
                sh '''
                    /opt/semgrep-venv/bin/semgrep scan \
                        --config auto \
                        --error \
                        application
                '''
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                    docker network create ${NET} 2>/dev/null || true
                    docker network connect ${NET} $(hostname) 2>/dev/null || true
                    docker rm -f ${CONTAINER} 2>/dev/null || true
                    docker run -d --name ${CONTAINER} --network ${NET} -p ${HOST_PORT}:80 ${IMAGE}:latest
                    docker ps --filter name=${CONTAINER}
                '''
            }
        }

        stage('Smoke test') {
            steps {
                sh '''
                    for i in $(seq 1 20); do
                        curl -sf -o /dev/null -w "HTTP %{http_code}\\n" http://${CONTAINER}:80/ && exit 0
                        sleep 2
                    done
                    docker logs ${CONTAINER}
                    exit 1
                '''
            }
        }

        stage('Tests de securite web - OWASP ZAP') {
            steps {
                sh '''
                    mkdir -p zap-reports
                    docker rm -f zap-scan 2>/dev/null || true
                    docker run --name zap-scan --network ${NET} \
                        ghcr.io/zaproxy/zaproxy:stable \
                        zap-baseline.py -t http://${CONTAINER}:80 -r zap-report.html -J zap-report.json -I || true
                    docker cp zap-scan:/zap/wrk/. zap-reports/
                    docker rm -f zap-scan
                    ls -l zap-reports
                '''
            }
            post {
                always { archiveArtifacts artifacts: 'zap-reports/*', allowEmptyArchive: true }
            }
        }
    }

    post {
        success {
            echo 'Pipeline termine avec succes.'
        }

        failure {
            sh 'docker logs --tail 50 ${CONTAINER} || true'
            echo 'Echec du pipeline.'
        }
    }
}
