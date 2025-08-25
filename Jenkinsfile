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
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                sh 'npm install --prefix bulletin-board-app'
            }
        }

        stage('Test') {
            steps {
                script {
                    def testExists = sh(script: "npm run | grep -q 'test'", returnStatus: true) == 0
                    if (testExists) {
                        sh 'npm test --prefix bulletin-board-app'
                    } else {
                        echo 'No tests defined'
                    }
                }
            }
        }

        stage('Docker Build & Push') {
            steps {
                script {
                    docker.withRegistry("https://${DOCKER_REGISTRY}", "${DOCKER_CREDENTIALS_ID}") {
                        def appImage = docker.build("${IMAGE_NAME}:${IMAGE_TAG}", "./bulletin-board-app")
                        appImage.push()
                        appImage.push('latest')
                    }
                }
            }
        }

        stage('Update Helm Values') {
            steps {
                sh """
                    sed -i 's|repository:.*|repository: ${IMAGE_NAME}|' helm/values.yaml
                    sed -i 's|tag:.*|tag: ${IMAGE_TAG}|' helm/values.yaml
                """
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
                sh 'argocd app sync node-bulletin-board'
            }
        }

    }

    post {
        always {
            cleanWs()
        }
    }
}
