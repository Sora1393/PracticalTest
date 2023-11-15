pipeline {
    agent any

    stages {
        stage('Checkout SCM') {
            steps {
                git 'https://github.com/Sora1393/JenkinsDependencyCheckTest.git'
            }
        }

        stage('OWASP Dependency-Check Vulnerabilities') {
            steps {
                script {
                    // Assuming you have OWASP Dependency-Check installed in Jenkins
                    // Run the OWASP Dependency-Check scanner
                    def odcHome = tool 'OWASP Dependency-Check Vulnerabilities'
                    bat "${odcHome}\\bin\\dependency-check.bat -n -f ALL --scan . --project OWASP --out ."
                }
            }
        }

        stage('SonarQube Scan') {
            steps {
                script {
                    // Run the SonarQube scanner
                    withSonarQubeEnv('SonarQube Server') {
                        bat "sonar-scanner.bat -D\"sonar.projectKey=OWASP\" -D\"sonar.sources=.\" -D\"sonar.host.url=http://127.0.0.1:9000\" -D\"sonar.login=sqp_58f1661efbd331b677fb5940d1bd5b6c56f133c4\""
                    }
                }
            }
        }
    }

    post {
        success {
            dependencyCheckPublisher pattern: 'dependency-check-report.xml'
        }
    }
}
