pipeline {
    agent any // This specifies that the pipeline can run on any available agent

    stages {
        // You can add other stages for building, testing, etc., before the dependency check
        stage('Build') {
            steps {
                echo 'Building...'
                // Add build commands here
            }
        }

        stage('OWASP Dependency-Check Vulnerabilities') {
            steps {
                script {
                    // Run the OWASP Dependency Check
                    dependencyCheck additionalArguments: ''' 
                        -o './'
                        -s './'
                        -f 'ALL' 
                        --prettyPrint''', odcInstallation: 'OWASP Dependency-Check Vulnerabilities'
                    
                    // Publish the report
                    dependencyCheckPublisher pattern: 'dependency-check-report.xml'
                }
            }
        }

        // Optionally, add more stages for deployment or further testing
        stage('Deploy') {
            steps {
                echo 'Deploying...'
                // Add deployment commands here
            }
        }
    }

    post {
        always {
            echo 'This will always run regardless of the build status.'
        }
        success {
            echo 'Build was successful!'
        }
        failure {
            echo 'Build failed!'
        }
    }
}
