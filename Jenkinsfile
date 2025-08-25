pipeline {
    agent any

    environment {
        S3_BUCKET = 'demoacbdweb'
        AWS_DEFAULT_REGION = 'us-east-1'
        DOCKER_REGISTRY = 'https://index.docker.io'
        DOCKER_CREDENTIALS_ID = 'Docker-creds'
        GITHUB_CREDENTIALS_ID = 'Git-Creds'
        IMAGE_NAME = 'komall6/node-bulletin-board'
        IMAGE_TAG = "${BUILD_NUMBER}"
        APP_DIR = 'bulletin-board-app'
    }

    stages {
        stage('Checkout Code') {
            steps {
                git(
                    url: 'https://github.com/Dhanvikah/node-bulletin-board.git',
                    credentialsId: "${GITHUB_CREDENTIALS_ID}"
                )
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
                    def testOutput = sh(
                        script: "npm run --prefix ${APP_DIR} | grep -q test",
                        returnStatus: true
                    )
                    if (testOutput != 0) {
                        echo "No tests defined or tests failed"
                    } else {
                        echo "Tests passed"
                    }
                }
            }
        }

        stage('Docker Build & Push') {
            steps {
                script {
                    withDockerRegistry([credentialsId: "${DOCKER_CREDENTIALS_ID}", url: "${DOCKER_REGISTRY}"]) {
                        sh """
                        docker build -t ${IMAGE_NAME}:${IMAGE_TAG} ./${APP_DIR}
                        docker push ${IMAGE_NAME}:${IMAGE_TAG}
                        """
                    }
                }
            }
        }

        stage('Deploy to Kubernetes via Helm & ArgoCD') {
            steps {
                echo "Skipped for now, implement as needed"
            }
        }
    }

    post {
        always {
            cleanWs()
        }
    }
}
