pipeline {
    agent any

    environment {
        EMAIL_RECIPIENT = 'chloe.xibei.cheng@gmail.com'
        STAGING_SERVER = 'staging-server-address'
        PRODUCTION_SERVER = 'production-server-address'
    }

    stages {
        stage('Build') {
            steps {
                echo "Stage 1: Build the code using Maven to compile and package the code."
                echo "Tool: Maven"
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo "Stage 2: Run unit tests by JUnit to ensure the code functions as expected and run integration tests by Selenium to ensure the different components of the application work together as expected."
                echo "Tools: JUnit, Selenium"
            }

            post {
                // Send email notification with test results
                success {
                    mail to: "${env.EMAIL_RECIPIENT}",
                        subject: "Unit and Integration Tests Successful!",
                        body: "Good news, the unit and integration tests completed successfully!"
                }
                failure {
                    mail to: "${env.EMAIL_RECIPIENT}",
                        subject: "Unit and Integration Tests Failed.",
                        body: "Unfortunately, the unit and integration tests failed. Please check the logs for details."
                }
            }

        }

        stage('Code Analysis') {
            steps {
                echo "Stage 3: Integrate SonarQube to analyse the code and ensure it meets industry standards."
                echo "Tool: SonarQube"
            }
        }

        stage('Security Scan') {
            steps {
                echo "Stage 4: Perform OWASP Dependency-Check on the code using a tool to identify any vulnerabilities."
                echo "Tool: OWASP Dependency-Check"
            }
           post {
                always {
                    // 发送安全扫描结果通知邮件
                    emailext (
                        to: "${env.EMAIL_RECIPIENT}",
                        subject: "Security Scan Results",
                        body: "安全扫描已完成。",
                        attachLog: true // 附上构建日志
                    )
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo "Stage 5: Deploy the application to a staging server: ${env.STAGING_SERVER} by AWS CLI."
                echo "Tool: AWS CLI"
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo "Stage 6: Run integration tests in the staging environment using Selenium, to ensure the application functions as expected in a production-like environment."
                echo "Tool: Selenium"
            }
        }

        stage('Deploy to Production') {
            steps {
                echo "Stage 7: Deploy the application to a production server: ${env.PRODUCTION_SERVER} by AWS CLI."
                echo "Tool: AWS CLI"
            }
        }
        stage('Complete') {
            steps {
                echo "Successful!"
            }
        }
    }
    
}
