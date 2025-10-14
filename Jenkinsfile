pipeline {
    agent any

    stages {
        stage('Code Scanning') {
            environment {
                scannerHome = tool 'CliScanner'
            }
            steps {
                withSonarQubeEnv('Local'){
                    nodejs(nodeJSInstallationName: 'NodeJS') {
                        echo "Start Scanning..."
                        sh "${scannerHome}/bin/sonar-scanner"
                    }
                }
            }
        }
        stage('Dependency Track Publisher') {
            steps {
                nodejs(nodeJSInstallationName: 'NodeJS') {
					echo "Install Cyclonedx Plugin"
                    sh "npm install -g @cyclonedx/bom"
					echo "Build Application"
                    sh "npm install"
					echo "Generate bom.xml"
                    sh "cyclonedx-node"
                }
                withCredentials([string(credentialsId: 'dt-api-key', variable: 'API_KEY')]) {
					echo "Publish SBOM"
                    dependencyTrackPublisher artifact: 'bom.xml', projectId: '7d3be162-1e60-4bb0-b008-b8380e2283bc', synchronous: true
                }
            }
        }

    }
}
