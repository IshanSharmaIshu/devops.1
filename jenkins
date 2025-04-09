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
                    sh 'ls -l' // Example command

                    sh '''#!/bin/bash
                    set +x
                    WORKSPACE="${WORKSPACE}"
                    LOG_FILE="${WORKSPACE}/logs/sample-logs.json"
                    mkdir -p "$(dirname "$LOG_FILE")"
                    exec > >(cat - >> "$LOG_FILE") 2>&1
                    set -x
                    echo "This log will be written to sample-logs.json"
                    ls -la
                    java -version
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
                    sh 'docker-compose up -d'
                }
            }
        }
    }
}
