pipeline {
    agent any

    stages {
        stage('Run Python Script') {
            steps {
                echo "Running Python Script..."
                sh '/home/zoey/Jenkins/python_scripts/python3 redfish_test.py profile_get.json'
            }
        }
        stage('Code Scanning') {
            environment {
                scannerHome = tool 'CliScanner'
            }
            steps {
                withSonarQubeEnv('SonarQube'){
                    echo "Start Scanning..."
                    sh "${scannerHome}/bin/sonar-scanner"
                }
            }
        }
    }
}
