pipeline {
    agent any

    stages {
        stage('Conditional Build') {
            when {
                expression {
                    return env.BRANCH_NAME == 'main' || env.BRANCH_NAME.startsWith('feature/')
                }
            }
            stages {
                stage('Checkout') {
                    steps {
                        checkout scm
                    }
                }

                stage('Restore dependencies') {
                    steps {
                        bat 'dotnet restore'
                    }
                }

                stage('Build') {
                    steps {
                        bat 'dotnet build --no-restore'
                    }
                }

                stage('Test') {
                    steps {
                        bat 'dotnet test --no-build --verbosity normal'
                    }
                }
            }
        }
    }

    post {
        always {
            echo "Pipeline finished for branch: ${env.BRANCH_NAME}"
        }
    }
}
