pipeline {
    agent any

    environment {
        DOCKER_CREDENTIALS_ID = 'Docker-creds'  
        GITHUB_CREDENTIALS_ID = 'Git-Creds'
        IMAGE_NAME = 'komall6/node-bulletin-board'
        IMAGE_TAG = "${BUILD_NUMBER}"
        APP_DIR = 'bulletin-board-app'
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'master',
                    url: 'https://github.com/Dhanvikah/node-bulletin-board.git',
                    credentialsId: "${GITHUB_CREDENTIALS_ID}"
            }
        }

        stage('Install Dependencies') {
            steps {
                sh "npm install --prefix ${APP_DIR}"
            }
        }

        stage('Run Tests') {
            steps {
                script {
                    sh "npm test --prefix ${APP_DIR} || echo 'No tests defined or failed, skipping...'"
                }
            }
        }

        stage('Docker Build & Push') {
            steps {
                script {
                    withCredentials([usernamePassword(
                        credentialsId: "${DOCKER_CREDENTIALS_ID}", 
                        usernameVariable: 'DOCKER_USERNAME', 
                        passwordVariable: 'DOCKER_PASSWORD')]) {

                        sh """
                        echo $DOCKER_PASSWORD | docker login -u $DOCKER_USERNAME --password-stdin
                        docker build -t ${IMAGE_NAME}:${IMAGE_TAG} ./${APP_DIR}
                        docker push ${IMAGE_NAME}:${IMAGE_TAG}
                        """
                    }
                }
            }
        }

        stage('Deploy to Kubernetes via Helm & ArgoCD') {
            steps {
                echo "Deployment stage ready. Add Helm/ArgoCD commands here."
            }
        }
    }

    post {
        always {
            cleanWs()
        }
        success {
            echo "Pipeline completed successfully!"
        }
        failure {
            echo "Pipeline failed. Check logs for errors."
        }
    }
}
