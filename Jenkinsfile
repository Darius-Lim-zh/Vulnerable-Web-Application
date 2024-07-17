pipeline {
  agent any
  stages {
    stage ('Checkout') {
      steps {
        git branch:'master', url: 'https://github.com/Darius-Lim-zh/Vulnerable-Web-Application.git'
      }
    }
    stage('Code Quality Check via SonarQube') {
      steps {
        script {
          def scannerHome = tool 'SonarQube';
            withSonarQubeEnv('SonarQube') {
              sh "${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=OWASP -Dsonar.sources=. -Dsonar.host.url=http://192.168.1.16:9000 -Dsonar.token=sqp_cc4b9c39d53a618907f333765d9219e73633f6d8"
            }
          }
        }
      }
    }
    post {
      always {
        recordIssues enabledForFailure: true, tool: sonarQube()
      }
    }
}
