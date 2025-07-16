pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Write Logs') {
            steps {
                script {
                    echo "Starting the pipeline..."
                    sh 'ls -l'
                    sh '''#!/bin/bash
                    set +x
                    WORKSPACE="${WORKSPACE}"
                    LOG_FILE="${WORKSPACE}/logs/sample-logs.json"
                    mkdir -p "$(dirname "$LOG_FILE")"
                    if [ -f "$LOG_FILE" ]; then
                        echo "Verifying committed sample-logs.json..."
                        cat "$LOG_FILE"
                    else
                        echo "Error: sample-logs.json not found in logs directory"
                        exit 1
                    fi
                    set -x
                    ls -la logs/
                    '''
                }
            }
        }
        stage('Another Stage (Optional)') {
            steps {
                echo "This is another stage."
            }
        }
        stage('Deploy Setup') {
            steps {
                script {
                    echo "Deploying the setup using Docker Compose..."
                    sh 'docker-compose down --volumes'
                    sh 'docker-compose up -d'
                }
            }
        }
    }
}
