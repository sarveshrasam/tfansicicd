pipeline {
        agent any
        tools {
                terraform 'Terraform'
        }

        environment {
        AWS_ACCESS_KEY_ID     = credentials('AWS_ACCESS_KEY_ID')
        AWS_SECRET_ACCESS_KEY = credentials('AWS_SECRET_ACCESS_KEY')
        }

        stages {
                stage('Git checkout'){
                        agent {
				label {
					label 'git-checkout'
					customworkspace '/var/lib/jenkins/workspace/cicdproject'
				}
                        }
                        steps {
                                git branch: 'main', credentialsId: 'github', url: 'https://github.com/sarveshrasam/cicdtest.git'
                        }
                }

                stage('Terraform init'){
                        agent {
                                label {
                                        label 'terraform-init'
                                        customworkspace '/var/lib/jenkins/workspace/cicdproject'
                                }
                        }
                        steps {
                                sh label: '', script: 'terraform init'
                        }
                }

                stage('Terraform apply'){
                        agent {
                                label {
                                        label 'terraform-apply'
                                        customworkspace '/var/lib/jenkins/workspace/cicdproject'
                                }
                        }
                        steps {
                                sh label: '', script: 'terraform apply --auto-approve'
                        }
                }

        }
}
