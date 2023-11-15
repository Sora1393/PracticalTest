pipeline {
    agent any

    stages {
        stage('Checkout SCM') {
            steps {
                git 'https://github.com/Sora1393/JenkinsDependencyCheckTest.git'
				sonar-scanner.bat -D"sonar.projectKey=OWASP" -D"sonar.sources=." -D"sonar.host.url=http://127.0.0.1:9000" -D"sonar.token=sqp_58f1661efbd331b677fb5940d1bd5b6c56f133c4"
            }
        }

        stage('OWASP Dependency-Check Vulnerabilities') {
            steps {
                script {
                    // Assuming you have OWASP Dependency-Check installed in Jenkins
                    dependencyCheck additionalArguments: ''' 
                        -o './'
                        -s './'
                        -f 'ALL' 
                        --prettyPrint
                        --suppression suppression.xml
                    ''', odcInstallation: 'OWASP Dependency-Check Vulnerabilities'
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
