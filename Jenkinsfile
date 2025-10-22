pipeline {
    agent any

    stages {
        
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
