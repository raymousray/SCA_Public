pipeline {
        agent {
        docker {
            image 'node:18.18.2-alpine3.18'
            args '-p 3000:3000'
        }
    }
    tools{
        jdk "JDK"
    }

    stages {
        stage('Checkout') {
            steps {
                // Check out the Git repository
                git branch: 'main', changelog: false, poll: false, url: 'https://github.com/ATISH0607/SCA_Public.git'
            }
        }
        
        stage('Build') {
            steps {
                 // Build your project (e.g., compile, package, etc.)
                sh 'mvn clean package'
            }
        }

        stage('Dependency-Check') {
            steps {
                // Invoke OWASP Dependency-Check
                // Ensure that OWASP Dependency-Check is available in the system PATH
                dependencyCheck additionalArguments: '--project WORKSPACE', odcInstallation: 'SCA'
                dependencyCheckPublisher pattern: 'dependency-check-report.xml'
            }
        }
    }
}
pipeline {
    agent any
    
    tools{
        jdk "JDK"
    }

    stages {
        stage('Checkout') {
            steps {
                // Check out the Git repository
                git branch: 'main', changelog: false, poll: false, url: 'https://github.com/ATISH0607/SCA_Public.git'
            }
        }
        
        stage('Build') {
            steps {
                 // Build your project (e.g., compile, package, etc.)
                sh 'mvn clean package'
            }
        }

        stage('Dependency-Check') {
            steps {
                // Invoke OWASP Dependency-Check
                // Ensure that OWASP Dependency-Check is available in the system PATH
                dependencyCheck additionalArguments: '--project WORKSPACE', odcInstallation: 'SCA'
                dependencyCheckPublisher pattern: 'dependency-check-report.xml'
            }
        }
    }
}
