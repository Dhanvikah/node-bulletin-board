pipeline {
  agent any

  environment {
    DOCKERHUB_CREDENTIALS = credentials('Docker-creds')
    IMAGE_NAME = "komall6/node-bulletin-board"
    IMAGE_TAG = "${BUILD_NUMBER}-${GIT_COMMIT.take(7)}"
  }

  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }

    stage('Build Docker image') {
      steps {
        script {
          sh """
            docker build \
              -t ${IMAGE_NAME}:${IMAGE_TAG} \
              -t ${IMAGE_NAME}:latest \
              -f bulletin-board-app/Dockerfile bulletin-board-app
          """
        }
      }
    }

    stage('Push Docker image') {
      steps {
        withCredentials([usernamePassword(credentialsId: 'Docker-creds', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
          sh """
            echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin
            docker push ${IMAGE_NAME}:${IMAGE_TAG}
            docker push ${IMAGE_NAME}:latest
          """
        }
      }
    }

    stage('Update Helm values & push to Git') {
      steps {
        dir('helm') {
          withCredentials([usernamePassword(credentialsId: 'Git-Creds', usernameVariable: 'GIT_USER', passwordVariable: 'GIT_TOKEN')]) {
            sh """
              sed -i 's/tag: .*/tag: "${IMAGE_TAG}"/' values.yaml || true

              git config user.email 'jenkins@ci.local'
              git config user.name 'jenkins'

              git remote set-url origin https://${GIT_USER}:${GIT_TOKEN}@github.com/Dhanvikah/node-bulletin-board.git

              git add values.yaml
              git commit -m 'ci: bump image tag to ${IMAGE_TAG}' || echo 'no changes to commit'
              branch=\$(git rev-parse --abbrev-ref HEAD)
              git push origin HEAD:\$branch
            """
          }
        }
      }
    }

    stage('Trigger ArgoCD Sync') {
      steps {
        sh "argocd app sync node-bulletin-board || true"
      }
    }
  }
}
