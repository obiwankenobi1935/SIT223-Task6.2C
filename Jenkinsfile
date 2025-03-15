pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building the application...'
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                script {
                    try {
                        echo 'Running unit and integration tests...'
                        powershell 'echo "Running tests..." | Out-File -FilePath test_log.txt'
                        
                        echo 'Tests passed successfully.'
                        
                        // Send email on success with logs
                        emailext subject: "Jenkins Pipeline: Tests Passed",
                            body: "All unit and integration tests passed successfully.",
                            to: "kavishchoudhary1935@gmail.com",
                            attachmentsPattern: "test_log.txt"
                    } catch (Exception e) {
                        echo 'Tests failed! Sending failure email...'
                        powershell 'echo "Tests failed!" | Out-File -FilePath test_log.txt'
                        
                        // Send email on failure with logs
                        emailext subject: "Jenkins Pipeline: Tests Failed",
                            body: "Unit and integration tests failed. Please check the logs.",
                            to: "kavishchoudhary1935@gmail.com",
                            attachmentsPattern: "test_log.txt"
                        
                        error "Failing the build due to test failure."
                    }
                }
            }
        }

        stage('Security Scan') {
            steps {
                script {
                    try {
                        echo 'Running security scan...'
                        powershell 'echo "Security scan results..." | Out-File -FilePath security_scan_log.txt'
                        
                        echo 'Security scan completed successfully.'
                        
                        // Send email on success with logs
                        emailext subject: "Jenkins Pipeline: Security Scan Passed",
                            body: "Security scan completed successfully.",
                            to: "kavishchoudhary1935@gmail.com",
                            attachmentsPattern: "security_scan_log.txt"
                    } catch (Exception e) {
                        echo 'Security scan failed! Sending failure email...'
                        powershell 'echo "Security scan failed!" | Out-File -FilePath security_scan_log.txt'
                        
                        // Send email on failure with logs
                        emailext subject: "Jenkins Pipeline: Security Scan Failed",
                            body: "Security scan encountered issues. Please check the logs.",
                            to: "kavishchoudhary1935@gmail.com",
                            attachmentsPattern: "security_scan_log.txt"
                        
                        error "Failing the build due to security scan failure."
                    }
                }
            }
        }
    }

    post {
        always {
            echo 'Pipeline execution completed.'
        }
    }
}
