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

        stage('SonarQube Scan') {
            steps {
                script {
                  sonar-scanner \
					-Dsonar.projectKey=OWASP \
					-Dsonar.sources=. \
					-Dsonar.host.url=http://127.0.0.1:9000 \
					-Dsonar.token=sqp_58f1661efbd331b677fb5940d1bd5b6c56f133c4
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
