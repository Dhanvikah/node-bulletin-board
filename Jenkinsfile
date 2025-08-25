pipeline {
    agent any

    environment {
        S3_BUCKET = 'demoacbdweb'
        AWS_DEFAULT_REGION = 'us-east-1'
        DOCKER_REGISTRY = 'index.docker.io'
        DOCKER_CREDENTIALS_ID = 'Docker-creds'
        GITHUB_CREDENTIALS_ID = 'Git-Creds'
        IMAGE_NAME = 'komall6/node-bulletin-board'
        IMAGE_TAG = "${BUILD_NUMBER}"
        APP_DIR = 'bulletin-board-app' // Added app directory variable
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                sh "npm install --prefix ${APP_DIR}"
            }
        }

        stage('Test') {
            steps {
                script {
                    // Check if package.json exists
                    if (fileExists("${APP_DIR}/package.json")) {
                        def testExists = sh(script: "npm run --prefix ${APP_DIR} | grep -q 'test'", returnStatus: true) == 0
                        if (testExists) {
                            sh "npm test --prefix ${APP_DIR}"
                        } else {
                            echo 'No tests defined'
                        }
                    } else {
                        echo "No package.json found in ${APP_DIR}, skipping tests"
                    }
                }
            }
        }

        stage('Docker Build & Push') {
            steps {
                script {
                    docker.withRegistry("https://${DOCKER_REGISTRY}", "${DOCKER_CREDENTIALS_ID}") {
                        def appImage = docker.build("${IMAGE_NAME}:${IMAGE_TAG}", "./${APP_DIR}")
                        appImage.push()
                        appImage.push('latest')
                    }
                }
            }
        }

        stage('Update Helm Values') {
            steps {
                script {
                    if (fileExists("helm/values.yaml")) {
                        sh """
                            sed -i 's|repository:.*|repository: ${IMAGE_NAME}|' helm/values.yaml
                            sed -i 's|tag:.*|tag: ${IMAGE_TAG}|' helm/values.yaml
                        """
                    } else {
                        echo "helm/values.yaml not found, skipping update"
                    }
                }
            }
        }

        stage('Git Commit & Push for ArgoCD Sync') {
            steps {
                withCredentials([string(credentialsId: "${GITHUB_CREDENTIALS_ID}", variable: 'GITHUB_TOKEN')]) {
                    sh """
                        git config user.email "jenkins@ci.com"
                        git config user.name "Jenkins"
                        git add helm/values.yaml
                        git diff --cached --quiet || git commit -m "Update image tag to ${IMAGE_TAG}"
                        git push https://$GITHUB_TOKEN@github.com/Dhanvikah/node-bulletin-board.git HEAD:master || echo "Nothing to push"
                    """
                }
            }
        }

        stage('Deploy via ArgoCD') {
            steps {
                sh 'argocd app sync node-bulletin-board || echo "ArgoCD sync failed, check manually"'
            }
        }

    }

    post {
        always {
            cleanWs()
        }
    }
}
