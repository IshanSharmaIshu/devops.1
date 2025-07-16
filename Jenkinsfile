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
        stage('Install Grafana Plugin') {
            steps {
                script {
                    sh 'java -jar jenkins-cli.jar -s http://localhost:8080/ install-plugin grafana'
                }
            }
        }
        stage('Configure Grafana Plugin') {
            steps {
                script {
                    sh '''#!/bin/bash
                    cat <<EOF > ${JENKINS_HOME}/grafana-config.xml
                    <hudson.plugins.grafana.GrafanaConfiguration>
                        <url>http://localhost:3000</url>
                        <apiKey>YOUR_API_KEY</apiKey>
                    </hudson.plugins.grafana.GrafanaConfiguration>
                    EOF
                    '''
                }
            }
        }
        stage('Send Logs to Grafana') {
            steps {
                script {
                    sh '''#!/bin/bash
                    curl -X POST -H "Content-Type: application/json" -H "Authorization: Bearer YOUR_API_KEY" -d @${WORKSPACE}/logs/sample-logs.json http://localhost:3000/api/live/push
                    '''
                }
            }
        }
    }
}
