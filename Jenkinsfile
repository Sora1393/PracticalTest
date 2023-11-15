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
    }

    post {
        success {
            dependencyCheckPublisher pattern: 'dependency-check-report.xml'
        }
    }
}
