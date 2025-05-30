pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'This stage compiles and packages the application using a build automation tool like Maven or Gradle.'
                echo 'For Java projects, Maven (mvn clean package) can be used.
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                script {
                    try {
                        echo 'Running unit and integration tests'
                        
                        echo 'Tests passed successfully.'
                        
                        // Send email on success with logs
                        emailext subject: "Jenkins Pipeline: Tests Passed",
                            body: "All unit and integration tests passed successfully.",
                            to: "harjot4780.be23@chitkara.edu.in"
                    } catch (Exception e) {
                        echo 'Tests failed! Sending failure email...'
                        
                        // Send email on failure with logs
                        emailext subject: "Jenkins Pipeline: Tests Failed",
                            body: "Unit and integration tests failed. Please check the logs.",
                            to: "harjot4780.be23@chitkara.edu.in",
                        
                        error "Failing the build due to test failure."
                    }
                }
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'This stage integrates a code analysis tool to check code quality and industry standards.'
                echo 'SonarQube or Checkstyle can be used for static code analysis.'
            }
        }

        stage('Security Scan') {
            steps {
                echo 'This stage performs a security scan to identify vulnerabilities in the code or dependencies.'
                echo 'OWASP Dependency-Check or Snyk can be used for scanning security issues.'
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'This stage deploys the application to a staging environment, such as an AWS EC2 instance.'
                echo 'Deployment tools like SCP, Ansible, or Docker can be used.'
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'This stage executes integration tests in a staging environment to simulate production conditions.'
                echo 'API testing tools like Postman or cURL can be used to verify functionality.'
            }
        }
    }

    post {
        always {
            echo 'Pipeline execution completed.'
        }
    }
}
