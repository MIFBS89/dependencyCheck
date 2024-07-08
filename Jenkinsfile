pipeline {
  agent any
  stages {
    stage('Checkout SCM') {
      steps {
        git url 'https://github.com/MIFBS89/dependencyCheck.git',
            branch: 'main'
      }
    }

    stage('OWASP DependencyCheck') {
      steps {
        dependencyCheck(additionalArguments: '--format HTML --format XML', odcInstallation: 'Default')
      }
    }

  }
  post {
    success {
      dependencyCheckPublisher(pattern: 'dependency-check-report.xml')
    }

  }
}
