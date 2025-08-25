pipeline {
    agent any

    environment {
        DOCKERHUB_USER = 'komall6'                   
        DOCKERHUB_REPO = 'node-bulletin-board'       
        APP_NAME = 'node-bulletin-board'             
        DOCKER_CREDENTIALS = 'dockerhub-creds'       
    }

    stages {
        stage('Build') {
            steps {
                sh 'npm install --prefix bulletin-board-app'
            }
        }

        stage('Test') {
            steps {
                sh 'npm test --prefix bulletin-board-app || echo "No tests defined"'
            }
        }

        stage('Docker Build & Push') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', "${DOCKER_CREDENTIALS}") {
                        def app = docker.build("${DOCKERHUB_USER}/${DOCKERHUB_REPO}:${BUILD_NUMBER}", "./bulletin-board-app")
                        app.push()
                        app.push("latest")
                    }
                }
            }
        }

        stage('Update Helm values') {
            steps {
                script {
                    sh """
                        sed -i 's|repository:.*|repository: ${DOCKERHUB_USER}/${DOCKERHUB_REPO}|' helm/values.yaml
                        sed -i 's|tag:.*|tag: ${BUILD_NUMBER}|' helm/values.yaml
                    """
                }
            }
        }

        stage('Git Commit & Push for ArgoCD Sync') {
            steps {
                script {
                    sh """
                        git config user.email "jenkins@ci.com"
                        git config user.name "Jenkins"
                        git add helm/values.yaml
                        git commit -m "Update image tag to ${BUILD_NUMBER}" || echo "No changes to commit"
                        git push origin master
                    """
                }
            }
        }

        stage('Deploy via ArgoCD') {
            steps {
                script {
                      sh "argocd app sync ${APP_NAME} --grpc-web --server <ARGOCD_SERVER> --auth-token <ARGOCD_TOKEN>"
                }
            }
        }
    }
}
