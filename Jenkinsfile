pipeline {
    agent any

    stages {
        stage('Git Checkout') {
            steps {
                git 'https://github.com/RajPractiseRepo/CountryBank.git'
            }
        }
        
        stage('OWASP Dependency Check') {
            steps {
                 dependencyCheck additionalArguments: ' --scan ./ ', odcInstallation: 'DC'
                    dependencyCheckPublisher pattern: '**/dependency-check-report.xml'
            }
        }

        stage('Trivy') {
            steps {
                 sh "trivy fs ."
            }
        }
        
         stage('Build & deploy') {
            steps {
                 sh "docker-compose up -d"
            }
        }
    }
}
        
