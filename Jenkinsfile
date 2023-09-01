pipeline {
    agent any

    environment {
        AWS_DEFAULT_REGION = 'us-east-1'
    }

    stages {
        stage('Debug') {
            steps {
                // Add debugging information
                sh 'git ls-remote -h origin'
            }
        }

        stage('Checkout Code') {
            steps {
                // Checkout your Terraform code repository specifying the branch
                git branch: 'main',  url: 'https://github.com/andonebekasi/testing-aws.git'
            }
        }

        stage('Terraform Init') {
            steps {
                script {
                    // Initialize Terraform in the workspace
                    sh 'terraform init -input=false'
                }
            }
        }

        stage('Terraform Apply') {
            steps {
                script {
                    // Apply the Terraform configuration to create the VPC
                    sh 'terraform apply -auto-approve'
                }
            }
        }
    }

    post {
        always {
            stage('Terraform Destroy (Cleanup)') {
                steps {
                    script {
                        // Destroy the VPC (cleanup) after the job completes
                        sh 'terraform destroy -auto-approve'
                    }
                }
            }
        }
    }
}
