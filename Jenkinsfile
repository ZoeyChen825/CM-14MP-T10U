pipeline {
    agent any

    stages {
        stage('Run Python Script') {
            steps {
                echo "Running Python Script..."
                sh 'python3 /home/zoey/Jenkins/python_scripts/redfish_test.py /home/zoey/Jenkins/python_scripts/profile_get.json'
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
